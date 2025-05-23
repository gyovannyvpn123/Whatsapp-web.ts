# 🚀 WhatsApp Web TypeScript Library

**Complete WhatsApp Web client library - Production ready alternative to Baileys.js**

[![TypeScript](https://img.shields.io/badge/TypeScript-Ready-blue)](https://github.com/gyovannyvpn123/Whatsapp-web.ts)
[![License](https://img.shields.io/badge/License-MIT-green.svg)](https://github.com/gyovannyvpn123/Whatsapp-web.ts/blob/main/LICENSE)
[![GitHub Stars](https://img.shields.io/github/stars/gyovannyvpn123/Whatsapp-web.ts)](https://github.com/gyovannyvpn123/Whatsapp-web.ts)

## 🌟 Features

- ✅ **Complete WhatsApp Web Protocol** - Full implementation
- 🔐 **Real Cryptography** - Curve25519, HKDF, AES-256-CBC
- 📱 **QR Code & Pairing** - ASCII QR codes + 8-digit pairing codes
- 💬 **All Message Types** - Text, media, documents, stickers, polls, reactions
- 👥 **Group Management** - Complete admin controls
- 🏢 **Business Features** - Catalogs, orders, payments
- 📞 **Calls Support** - Voice and video calls
- 📱 **Status/Stories** - Complete status functionality
- 🔄 **Auto-Reconnection** - Robust connection management
- 📊 **Full TypeScript** - Complete type safety

## 📦 Quick Start

```typescript
import { WhatsAppClient } from './src/WhatsAppClient';

const client = new WhatsAppClient({
  enableLogging: true,
  reconnectAttempts: 5
});

// QR Code authentication
client.on('qr_code', (qr) => {
  console.log('Scan this QR with WhatsApp:');
  console.log(qr.qrString);
});

// Authentication success
client.on('authenticated', (session) => {
  console.log('WhatsApp Web connected!', session.wid);
});

// Incoming messages
client.on('message', (message) => {
  console.log('New message:', message.body);
  
  if (message.body === 'ping') {
    client.sendMessage(message.chatId, 'pong! 🏓');
  }
});

// Connect to WhatsApp
await client.connect();

// Send messages
await client.sendMessage('1234567890@s.whatsapp.net', 'Hello World! 🌍');

// Send media
const imageBuffer = fs.readFileSync('image.jpg');
await client.sendImage('1234567890@s.whatsapp.net', imageBuffer, 'Check this out!');

// Create group
const groupId = await client.createGroup('My Group', [
  '1234567890@s.whatsapp.net',
  '0987654321@s.whatsapp.net'
]);
```

## 🔐 Authentication Methods

### QR Code Authentication
```typescript
client.on('qr_code', (qr) => {
  // Display ASCII QR code in terminal
  console.log(qr.qrString);
  
  // QR expires automatically after 60 seconds
  console.log('QR expires at:', new Date(qr.expiresAt));
});
```

## 💬 Message Examples

### Text Messages
```typescript
await client.sendMessage(chatId, 'Hello World!');
```

### Media Messages
```typescript
// Images
await client.sendImage(chatId, imageBuffer, 'Caption');

// Videos  
await client.sendVideo(chatId, videoBuffer, 'Video caption');

// Audio
await client.sendAudio(chatId, audioBuffer);

// Documents
await client.sendDocument(chatId, docBuffer, 'document.pdf');
```

## 👥 Group Management

```typescript
// Create group
const groupId = await client.createGroup('Group Name', participants);

// Add participants
await client.addParticipants(groupId, ['user@s.whatsapp.net']);

// Update group info
await client.updateGroupInfo(groupId, {
  name: 'New Group Name',
  description: 'Group description'
});
```

## 🔄 Connection Management

```typescript
// Connection events
client.on('connected', () => {
  console.log('Connected to WhatsApp');
});

client.on('disconnected', ({ code, reason }) => {
  console.log('Disconnected:', reason);
});

client.on('reconnecting', (attempt) => {
  console.log(`Reconnecting attempt ${attempt}...`);
});

// Manual reconnection
await client.reconnect();

// Graceful disconnect
await client.disconnect();
```

## ⚙️ Configuration

```typescript
const client = new WhatsAppClient({
  // Connection settings
  reconnectAttempts: 5,
  reconnectDelay: 3000,
  timeout: 30000,
  
  // Logging
  enableLogging: true,
  
  // Custom endpoints
  wsEndpoint: 'wss://web.whatsapp.com/ws',
  userAgent: 'Custom WhatsApp Web Client'
});
```

## 📊 Production Ready

This library is battle-tested and production ready:

- ✅ Real WhatsApp protocol implementation
- ✅ Production-grade error handling  
- ✅ Complete TypeScript definitions
- ✅ Comprehensive testing
- ✅ Active maintenance

## 🆚 vs Baileys

| Feature | This Library | Baileys |
|---------|-------------|---------|
| TypeScript | ✅ Native | ✅ Yes |
| QR Authentication | ✅ ASCII QR | ✅ Yes |
| Binary Protocol | ✅ Real implementation | ✅ Yes |
| Business Features | ✅ Complete | ⚠️ Limited |
| Documentation | ✅ Comprehensive | ⚠️ Basic |
| Bundle Size | ✅ Optimized | ⚠️ Large |

## 📄 License

MIT License - see [LICENSE](LICENSE) file for details.

## ⚠️ Disclaimer

This library is not affiliated with WhatsApp Inc. Use responsibly and comply with WhatsApp's Terms of Service.

---

Made with ❤️ for the WhatsApp automation community
