# Kanizsa API Gateway

**Version:** 2.1.0  
**Last Updated:** August 9, 2025, 12:06:39 CDT  
**Purpose:** Centralized API Gateway & Infrastructure Services for Kanizsa Ecosystem

## 🎯 **Overview**

The Kanizsa API Gateway serves as the central entry point for all external requests to the Kanizsa ecosystem. It provides routing, load balancing, authentication, rate limiting, and monitoring capabilities for all downstream services.

## 🏗️ **Architecture**

```
┌─────────────────┐    ┌─────────────────┐    ┌─────────────────┐
│   External      │    │   API Gateway   │    │   Kanizsa       │
│   Clients       │───▶│   (Kong)        │───▶│   Services      │
│                 │    │                 │    │                 │
└─────────────────┘    └─────────────────┘    └─────────────────┘
                                │
                                ▼
                       ┌─────────────────┐
                       │   Redis &       │
                       │   Celery        │
                       └─────────────────┘
```

## 🚀 **Quick Start**

### Prerequisites
- Docker and Docker Compose
- At least 2GB RAM available

### Containerized Setup
```bash
# Clone the repository
git clone https://github.com/wcervin/kanizsa-api-gateway.git
cd kanizsa-api-gateway

# Copy environment variables
cp env.example .env

# Start the API gateway stack
docker-compose up -d

# Access services
# Kong Admin API: http://localhost:8001
# Kong Proxy: http://localhost:8000
# Health Check: http://localhost:8080/health
```

## 🔧 **Gateway Services**

### **Kong Gateway**
- **Purpose:** API gateway and proxy
- **Ports:** 8000 (Proxy), 8001 (Admin)
- **Features:**
  - Request routing
  - Load balancing
  - Rate limiting
  - Authentication
  - Request/response transformation

### **Redis Cache**
- **Purpose:** Caching and session storage
- **Port:** 6379
- **Features:**
  - Response caching
  - Session management
  - Rate limiting storage
  - Distributed locking

### **Celery Task Processing**
- **Purpose:** Asynchronous task processing
- **Features:**
  - Background job processing
  - Task queuing
  - Distributed task execution
  - Task monitoring

### **Health Check Service**
- **Purpose:** Service health monitoring
- **Port:** 8080
- **Features:**
  - Service health checks
  - Dependency monitoring
  - Health status reporting
  - Alert generation

## �� **Configuration**

### Environment Variables
```bash
# Redis Configuration
REDIS_PASSWORD=kanizsa_redis_2025
REDIS_URL=redis://:kanizsa_redis_2025@redis:6379/0

# Celery Configuration
CELERY_BROKER_URL=redis://:kanizsa_redis_2025@redis:6379/0
CELERY_RESULT_BACKEND=redis://:kanizsa_redis_2025@redis:6379/0

# Health Check Service
PORT=8080
FLASK_DEBUG=false

# Kong Configuration
KONG_DATABASE=off
KONG_DECLARATIVE_CONFIG=/var/lib/kong/kong.yml
KONG_PROXY_LISTEN=0.0.0.0:8000, 0.0.0.0:8443 ssl
KONG_ADMIN_LISTEN=0.0.0.0:8001
```

## 🔍 **Gateway Capabilities**

### **Request Routing**
- Path-based routing
- Host-based routing
- Header-based routing
- Query parameter routing
- Service discovery

### **Load Balancing**
- Round-robin load balancing
- Least connections
- IP hash load balancing
- Health check-based routing
- Failover support

### **Rate Limiting**
- Request rate limiting
- IP-based limiting
- User-based limiting
- Burst protection
- Custom rate limit policies

### **Authentication**
- API key authentication
- JWT token validation
- OAuth2 integration
- Basic authentication
- Custom authentication plugins

### **Caching**
- Response caching
- Cache invalidation
- Cache warming
- Conditional caching
- Cache analytics

## 🔒 **Security**

### **Access Control**
- API key management
- Rate limiting
- IP whitelisting
- Request validation
- Security headers

### **Data Protection**
- SSL/TLS termination
- Request encryption
- Response encryption
- Audit logging
- Security monitoring

## 🚨 **Monitoring**

### **Gateway Monitoring**
- Request/response metrics
- Error rate tracking
- Latency monitoring
- Throughput metrics
- Health status

### **Service Monitoring**
- Upstream service health
- Dependency monitoring
- Circuit breaker status
- Performance analytics
- Alert generation

## 🚀 **Deployment**

### **Production Deployment**
```bash
# Production environment setup
docker-compose -f docker-compose.yml -f docker-compose.prod.yml up -d

# Scale services
docker-compose up -d --scale kong=3
```

### **High Availability**
- Kong cluster deployment
- Redis cluster setup
- Celery worker scaling
- Load balancer configuration
- Backup and recovery

## 🧪 **Testing**

### **Health Checks**
```bash
# Check gateway health
curl http://localhost:8080/health

# Check Kong status
curl http://localhost:8001/status

# Check Redis
redis-cli -h localhost -p 6379 ping
```

### **API Testing**
```bash
# Test proxy routing
curl http://localhost:8000/api/v1/health

# Test rate limiting
for i in {1..10}; do curl http://localhost:8000/api/v1/test; done
```

## 📚 **Documentation**

- [Kong Documentation](https://docs.konghq.com/)
- [Redis Documentation](https://redis.io/documentation)
- [Celery Documentation](https://docs.celeryproject.org/)
- [Kanizsa Ecosystem Documentation](../kanizsa-photo-categorizer/README.md)

## 🤝 **Contributing**

1. Fork the repository
2. Create a feature branch
3. Make your changes
4. Add tests
5. Submit a pull request

## 📄 **License**

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

---

**Footer:** Kanizsa API Gateway v2.1.0 | Last Updated: August 9, 2025, 12:06:39 CDT
