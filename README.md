# Load Balancer Visualization Demo

A simple demonstration of load balancing using HAProxy with multiple FastAPI backend servers and a visual frontend.

## Overview

This project demonstrates how a load balancer distributes traffic across multiple backend servers. It includes:

- 4 identical FastAPI backend servers
- HAProxy as the load balancer (using round-robin algorithm)
- A web-based visualization UI

## Architecture

```
                   ┌─────────┐
                   │ Browser │
                   └────┬────┘
                        │
                        ▼
┌───────────┐     ┌──────────┐     ┌─────────┐
│ Frontend  │◄────┤  HAProxy │◄────┤ Backend │
│ (Nginx)   │     │          │     │ Servers │
└───────────┘     └──────────┘     └─────────┘
```

## Getting Started

### Prerequisites

- Docker and Docker Compose

### Running the Application

1. Clone this repository
   ```
   git clone https://github.com/yourusername/load-balancer-demo.git
   cd load-balancer-demo
   ```

2. Start all services
   ```
   docker-compose up -d
   ```

3. Access the visualization UI
   ```
   http://localhost:3000
   ```

## How It Works

1. The frontend UI is served by Nginx on port 3000
2. When you click "Send Request", the UI makes an HTTP request to HAProxy (port 8080)
3. HAProxy routes the request to one of the four backend servers using round-robin
4. The UI highlights which server responded and displays the response data

## Components

- **Backend Servers**: Four identical FastAPI applications running on separate containers
- **HAProxy**: Load balancer configured with round-robin algorithm
- **Frontend**: Simple HTML/CSS/JS interface to visualize the load balancing

## Configuration Files

- `docker-compose.yml`: Defines all services and their relationships
- `haproxy/haproxy.cfg`: HAProxy configuration with load balancing settings
- `server1-4/main.py`: FastAPI application code
- `frontend/index.html`: Visualization interface

## Customization

### Changing Load Balancing Algorithm

Edit `haproxy/haproxy.cfg` and modify the `balance` directive:

```
backend servers
    balance roundrobin  # Change to: leastconn, source, etc.
```

### Adding More Servers

1. Add a new service in `docker-compose.yml`
2. Add the server to `haproxy/haproxy.cfg`
3. Update the frontend UI to include the new server

## License

MIT