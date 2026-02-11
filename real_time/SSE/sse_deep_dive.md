# Server-Sent Events (SSE) – Deep Dive

## 1. What is SSE?
Server-Sent Events (SSE) is a technology that allows a server to push real-time updates to clients over HTTP.
- Unidirectional: Server → Client
- Persistent connection for continuous updates
- Text-based event stream
- Automatic reconnection if connection drops

## 2. SSE vs WebSockets
| Feature | SSE | WebSockets |
|---------|-----|------------|
| Direction | Server → Client | Bidirectional |
| Protocol | HTTP/1.1 | WS/WSS |
| Browser support | Most modern browsers | Most modern browsers |
| Use case | Live feeds, notifications | Chat apps, multiplayer games |
| Complexity | Simple | More complex |
| Reconnection | Built-in | Manual |

## 3. SSE Protocol & Event Format
SSE uses `text/event-stream` format.
- Each message: `data:` prefix
- Messages separated by blank line
- Optional fields: `id:`, `event:`, `retry:`

Example:
```
id: 1
event: message
data: Hello World

id: 2
event: message
data: Another update
```

## 4. Client-Side Usage
```javascript
const evtSource = new EventSource("https://example.com/stream");
evtSource.onmessage = (event) => console.log("New message:", event.data);
evtSource.addEventListener("message", (event) => console.log("Custom event:", event.data));
evtSource.onerror = (err) => console.error("SSE error:", err);
```

## 5. Server-Side Implementation
```javascript
const http = require('http');
http.createServer((req, res) => {
  if (req.url === '/stream') {
    res.writeHead(200, {
      'Content-Type': 'text/event-stream',
      'Cache-Control': 'no-cache',
      'Connection': 'keep-alive'
    });

    let counter = 0;
    const interval = setInterval(() => {
      counter++;
      res.write(`id: ${counter}\n`);
      res.write(`event: message\n`);
      res.write(`data: This is update ${counter}\n\n`);
    }, 2000);

    req.on('close', () => clearInterval(interval));
  }
}).listen(3000, () => console.log('SSE server running on port 3000'));
```

## 6. Advantages of SSE
- Simple over HTTP
- Automatic reconnection
- Lightweight and text-based
- Great for live feeds and notifications

## 7. Limitations of SSE
- Unidirectional
- Each client keeps an open connection (scaling issue)
- Limited browser support for older browsers
- No native binary support

## 8. Use Cases
- Real-time dashboards
- Stock and crypto updates
- Social media/news feeds
- Web notifications

**Summary:** SSE is perfect for simple one-way real-time updates, while WebSockets suit bidirectional interactive apps.

