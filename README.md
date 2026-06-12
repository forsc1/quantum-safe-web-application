# Quantum-Safe Web Application

A comprehensive web application demonstrating post-quantum cryptographic implementations designed to be secure against both classical and quantum computer attacks.

## 🚀 Quick Start

```bash
# Clone and deploy
git clone <repository-url>
cd QuantumSafeWebApplications
docker-compose up -d

# Access application
open http://localhost:5000
```

## 📋 Features

- **🔐 Post-Quantum TLS**: Kyber768 KEM + Dilithium3 signatures
- **📨 Quantum-Safe Messaging**: ChaCha20-Poly1305 encryption  
- **💾 Secure Database**: BLAKE2s + SHA-3 dual hashing
- **🧪 Algorithm Demos**: Interactive cryptographic demonstrations
- **📊 Real-time Dashboard**: System monitoring and statistics

## 🌐 Application URLs

- **Main Application**: http://localhost:5000
- **📚 Documentation**: http://localhost:5000/docs
- **🔐 TLS Demo**: http://localhost:5000/tls  
- **📨 Messaging Demo**: http://localhost:5000/messaging
- **🧪 Algorithm Demo**: http://localhost:5000/demo
- **📊 Dashboard**: http://localhost:5000/dashboard

## 🔒 Quantum-Safe Algorithms

### Key Exchange Mechanisms (KEM)
- **Kyber768** (NIST Level 3) - Lattice-based cryptography
- **1,184 bytes** public key, **1,088 bytes** ciphertext

### Digital Signatures  
- **Dilithium3** (NIST Standardized) - Lattice-based signatures
- **1,952 bytes** public key, **3,293 bytes** signature

### Symmetric Encryption
- **ChaCha20-Poly1305** - Stream cipher with authentication
- **AES-256-CBC/GCM** - Block cipher for compatibility

### Hash Functions
- **BLAKE2s-256** - Quantum-resistant hashing
- **SHA-3-256** - Keccak sponge function
- **Container Orchestration**: Docker Compose setup with database and caching support
- **Production Ready**: Nginx reverse proxy with security headers and rate limiting

## 🏗 Architecture

```
┌─────────────────┐    ┌──────────────────┐    ┌───────────────────┐
│   Nginx Proxy   │───▶│  Flask Web App   │───▶│  liboqs Library   │
│  (Port 80/443)  │    │   (Port 5000)    │    │   (PQC Crypto)    │
└─────────────────┘    └──────────────────┘    └───────────────────┘
         │                        │                        │
         ▼                        ▼                        ▼
┌─────────────────┐    ┌──────────────────┐    ┌───────────────────┐
│  SSL/TLS with   │    │   PostgreSQL     │    │  Redis Cache      │
│ Post-Quantum    │    │   Database       │    │   & Sessions      │
│   Certificates  │    │  (Port 5432)     │    │  (Port 6379)      │
└─────────────────┘    └──────────────────┘    └───────────────────┘
```

## 🚀 Quick Start

### Prerequisites

- Docker Engine 20.10+
- Docker Compose 2.0+
- At least 4GB RAM available for containers
- Ports 80, 443, 5000, 5432, 6379 available

### Installation

1. **Clone or download this repository**:
   ```bash
   git clone <repository-url>
   cd QuantumSafeWebApplications
   ```

2. **Build and start the containers**:
   ```bash
   # Build the quantum-safe web application container
   docker-compose build
   
   # Start all services
   docker-compose up -d
   ```

3. **Generate SSL certificates** (for HTTPS):
   ```bash
   # Generate development certificates
   docker-compose exec quantum-safe-web bash /etc/config/generate-certs.sh
   
   # Restart nginx to load certificates
   docker-compose restart quantum-safe-web
   ```

4. **Access the application**:
   - **HTTP**: http://localhost
   - **HTTPS**: https://localhost (with self-signed cert warning)
   - **Direct Flask**: http://localhost:5000

### First Time Setup

The application will be available immediately, but for the full experience:

1. Wait for the containers to fully initialize (30-60 seconds)
2. Check the health endpoint: http://localhost:5000/health
3. Visit the dashboard to see supported algorithms: http://localhost/dashboard
4. Try the interactive demo: http://localhost/demo

## 📚 Usage Examples

### Web Interface

#### Dashboard
Visit `/dashboard` to see:
- System status and health metrics
- List of supported KEM and signature algorithms
- Performance comparisons
- Security level indicators

#### Interactive Demo
Visit `/demo` to:
- Test Key Encapsulation Mechanisms (Kyber, etc.)
- Generate and verify digital signatures (Dilithium, Falcon)
- Generate quantum-safe key pairs
- Compare algorithm performance

### API Endpoints

#### Get Supported Algorithms
```bash
curl http://localhost:5000/api/algorithms
```

#### Test Key Encapsulation
```bash
curl -X POST http://localhost:5000/api/demo/kem \
  -H "Content-Type: application/json" \
  -d '{"algorithm": "Kyber512"}'
```

#### Test Digital Signature
```bash
curl -X POST http://localhost:5000/api/demo/signature \
  -H "Content-Type: application/json" \
  -d '{"algorithm": "Dilithium2"}'
```

#### Generate Key Pairs
```bash
curl -X POST http://localhost:5000/api/generate-keys \
  -H "Content-Type: application/json" \
  -d '{"kem_algorithm": "Kyber768", "sig_algorithm": "Dilithium3"}'
```

## 🧪 Supported Algorithms

### Key Encapsulation Mechanisms (KEM)
- **Kyber512** - NIST Level 1 security (~128-bit)
- **Kyber768** - NIST Level 3 security (~192-bit) 
- **Kyber1024** - NIST Level 5 security (~256-bit)
- Additional algorithms available via liboqs

### Digital Signature Schemes
- **Dilithium2** - NIST Level 1 security
- **Dilithium3** - NIST Level 3 security  
- **Dilithium5** - NIST Level 5 security
- **Falcon-512** - NIST Level 1 security
- **Falcon-1024** - NIST Level 5 security
- Additional algorithms available via liboqs

### Hash-Based Signatures
- **SPHINCS+** variants (multiple parameter sets)
- **XMSS** and **LMS** (stateful schemes)

## 🔧 Configuration

### Environment Variables

Create a `.env` file to customize configuration:

```bash
# Flask Configuration
FLASK_ENV=production
FLASK_DEBUG=false
SECRET_KEY=your-super-secret-key-here

# Database Configuration  
POSTGRES_DB=quantumsafe
POSTGRES_USER=qsafe_user
POSTGRES_PASSWORD=secure-password

# SSL/TLS Configuration
SSL_CERT_PATH=/app/certs/server.crt
SSL_KEY_PATH=/app/certs/server.key

# Security Settings
RATE_LIMIT_API=10
RATE_LIMIT_STATIC=30
```

### Custom Algorithm Configuration

To enable/disable specific algorithms, modify the Python application or use environment variables:

```bash
# Enable only specific KEM algorithms
ENABLED_KEMS="Kyber512,Kyber768,Kyber1024"

# Enable only specific signature algorithms  
ENABLED_SIGS="Dilithium2,Dilithium3,Falcon-512"
```

## 🛠 Development

### Local Development Setup

1. **Install Python dependencies locally**:
   ```bash
   pip install -r requirements.txt
   ```

2. **Run the Flask app directly**:
   ```bash
   cd app
   python run.py
   ```

3. **Development with hot reload**:
   ```bash
   # Mount local code directory
   docker-compose -f docker-compose.yml -f docker-compose.dev.yml up
   ```

### Building Custom Images

```bash
# Build with specific liboqs version
docker build --build-arg LIBOQS_VERSION=0.9.0 -t quantum-safe-web:custom .

# Build for production
docker build --build-arg FLASK_ENV=production -t quantum-safe-web:prod .
```

## 📊 Performance Considerations

### Resource Requirements

- **Memory**: 2-4GB RAM recommended
- **CPU**: 2+ cores for optimal performance  
- **Storage**: 1GB+ for containers and data
- **Network**: Standard web application requirements

### Algorithm Performance Comparison

| Algorithm | Key Size | Signature Size | Sign Time | Verify Time |
|-----------|----------|----------------|-----------|-------------|
| Dilithium2 | 1.3KB | 2.4KB | ~0.1ms | ~0.1ms |
| Dilithium3 | 1.9KB | 3.3KB | ~0.2ms | ~0.2ms |
| Falcon-512 | 0.9KB | 0.7KB | ~8ms | ~0.1ms |
| Kyber512 | 0.8KB | 0.8KB | ~0.1ms | ~0.1ms |

*Performance varies by hardware and implementation*

## 🔒 Security Considerations

### Production Deployment

1. **Use proper SSL certificates**: Replace self-signed certificates with CA-issued certificates
2. **Configure firewalls**: Limit access to necessary ports only
3. **Update regularly**: Keep liboqs and dependencies updated
4. **Monitor logs**: Enable comprehensive logging and monitoring
5. **Rate limiting**: Configure appropriate rate limits for your use case

### Known Limitations

- Self-signed certificates for development only
- Some algorithms are research implementations
- Performance may vary significantly between algorithms
- Not all algorithms are NIST-standardized (yet)

## 🐛 Troubleshooting

### Common Issues

1. **Port conflicts**:
   ```bash
   # Check for port usage
   netstat -tlnp | grep :80
   netstat -tlnp | grep :443
   ```

2. **Container build failures**:
   ```bash
   # Clean build without cache
   docker-compose build --no-cache
   ```

3. **SSL certificate issues**:
   ```bash
   # Regenerate certificates
   docker-compose exec quantum-safe-web bash /etc/config/generate-certs.sh
   ```

4. **Algorithm not found errors**:
   ```bash
   # Check available algorithms
   docker-compose exec quantum-safe-web python -c "import oqs; print(oqs.get_enabled_KEM_mechanisms())"
   ```

### Debugging

Enable debug mode:
```bash
# Set debug environment
export FLASK_DEBUG=1
docker-compose up
```

Check container logs:
```bash
# View all logs
docker-compose logs

# Follow specific service logs
docker-compose logs -f quantum-safe-web
```

## 📖 References

- [Open Quantum Safe Project](https://openquantumsafe.org/)
- [liboqs Documentation](https://github.com/open-quantum-safe/liboqs)
- [NIST Post-Quantum Cryptography](https://csrc.nist.gov/projects/post-quantum-cryptography)
- [Quantum-Safe Security Working Group](https://datatracker.ietf.org/wg/qirg/about/)

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 🤝 Contributing

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

## 📞 Support

- Create an issue on GitHub for bug reports
- Check the [FAQ section](#-troubleshooting) for common problems
- Review container logs for debugging information

---

**⚠️ Important Note**: This is a demonstration and educational project. For production use, ensure proper security auditing, use certified implementations, and follow your organization's security guidelines.