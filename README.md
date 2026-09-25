# Linkzo Live

A real-time, browser-based video conferencing application built with WebRTC, Node.js, Express.js, and Socket.IO. Linkzo Live enables multiple participants to join a shared meeting room using a Room ID and communicate through peer-to-peer video and audio, real-time chat, screen sharing, and interactive meeting controls.

## Overview

Linkzo Live is designed as a lightweight real-time communication platform that operates directly through modern web browsers without requiring additional software installation.

The application uses a hybrid communication architecture:

- **WebRTC** handles peer-to-peer audio and video communication.
- **Node.js + Express.js** provide the application and signaling server.
- **Socket.IO** manages real-time signaling and room communication.
- **STUN/ICE** mechanisms help discover suitable network paths.
- **TURN servers** provide relay-based connectivity when direct peer-to-peer communication is restricted by NAT or network conditions.

The signaling server coordinates the connection establishment process but does not handle the actual media streams once the WebRTC peer connection is established.

## Features

### Real-Time Communication

- Peer-to-peer video communication using WebRTC
- Peer-to-peer audio communication
- Multi-participant meeting rooms
- Room-based joining using a Room ID
- Real-time participant count

### Media Controls

- Microphone mute/unmute
- Camera on/off
- Screen sharing
- Participant microphone status
- Participant camera status
- Focus mode / participant spotlight
- Fullscreen video viewing
- Picture-in-Picture (PiP) support
- Real-time call timer

### Real-Time Messaging

- Group chat within meeting rooms
- Private messaging between participants
- Sender name and timestamp information
- Real-time message delivery
- Private-message notifications and unread tracking

### Network Connectivity

- SDP offer/answer negotiation
- ICE candidate exchange
- STUN-based connectivity discovery
- Direct peer-to-peer media transmission when possible
- TURN relay fallback for restricted networks
- Multi-TURN fallback strategy for improved cross-network connectivity

## System Architecture

Linkzo Live follows a hybrid architecture consisting of a signaling layer and a peer-to-peer media layer.


                         ┌─────────────────────────┐
                         │   Node.js + Socket.IO   │
                         │    Signaling Server     │
                         └────────────┬────────────┘
                                      │
                         SDP / ICE / Room Events
                                      │
                     ┌────────────────┴────────────────┐
                     │                                 │
                     ▼                                 ▼
              ┌─────────────┐                   ┌─────────────┐
              │   Client A  │◄──── WebRTC ────►│   Client B  │
              │   Browser   │   P2P Media      │   Browser   │
              └─────────────┘                   └─────────────┘
