# Snippetbox

A web application for sharing code snippets, built with Go following the "Let's Go" book by Alex Edwards.

## About

Snippetbox is a full-featured web application that allows users to create, view, and share code snippets. This project serves as a comprehensive introduction to web development in Go, covering essential concepts like HTTP routing, templating, database integration, user authentication, and security best practices.

## Features

- **Create Snippets**: Users can create and save code snippets with syntax highlighting
- **View Snippets**: Browse and view individual code snippets
- **User Authentication**: Secure user registration and login system
- **Session Management**: Persistent user sessions with secure cookie handling
- **HTTPS Support**: TLS encryption for secure communication
- **Middleware**: Custom middleware for logging, security headers, and authentication
- **Database Integration**: MySQL database for persistent data storage
- **Input Validation**: Server-side form validation with user feedback
- **Security Features**: CSRF protection, secure headers, and input sanitization

## Technology Stack

- **Backend**: Go (Golang) with standard library
- **Database**: MySQL
- **Templates**: Go's `html/template` package
- **CSS Framework**: Custom CSS with responsive design
- **Security**: bcrypt for password hashing, CSRF tokens

## Project Structure

```
snippetbox/
├── cmd/
│   └── web/                    # Application entry point
│       ├── handlers.go         # HTTP handlers
│       ├── helpers.go          # Helper functions
│       ├── main.go            # Main function and server setup
│       ├── middleware.go      # Custom middleware
│       └── routes.go          # Route definitions
├── internal/
│   ├── models/                # Data models and database logic
│   └── validator/             # Input validation logic
├── ui/
│   ├── html/                  # HTML templates
│   │   ├── pages/            # Page templates
│   │   ├── partials/         # Partial templates
│   │   └── base.tmpl         # Base layout template
│   └── static/               # Static assets
│       ├── css/
│       ├── img/
│       └── js/
└── tls/                      # TLS certificates for HTTPS
```

## Prerequisites

Before running this application, make sure you have:

- **Go 1.21+** installed on your system
- **MySQL 8.0+** database server
- Basic familiarity with Go and web development concepts

## Installation

1. **Clone the repository**
   ```bash
   git clone https://github.com/yourusername/snippetbox.git
   cd snippetbox
   ```

2. **Set up the database**
   ```sql
   CREATE DATABASE snippetbox CHARACTER SET utf8mb4 COLLATE utf8mb4_unicode_ci;
   ```

   Run the SQL migrations found in the book or create the necessary tables:
   - `snippets` table for storing code snippets
   - `users` table for user accounts
   - `sessions` table for session management

3. **Configure environment variables** (or use command-line flags)
   ```bash
   export SNIPPETBOX_DSN="username:password@/snippetbox?parseTime=true"
   ```

## Usage

### Development Mode

Run the application in development mode:

```bash
go run ./cmd/web
```

The application will start on `http://localhost:4000` by default.

### Production Mode

For production deployment with HTTPS:

```bash
go run ./cmd/web -addr=":443" -dsn="your-database-dsn" -tls-cert="./tls/cert.pem" -tls-key="./tls/key.pem"
```

### Command-line Flags

- `-addr`: Server address (default: ":4000")
- `-dsn`: MySQL database DSN
- `-tls-cert`: Path to TLS certificate file
- `-tls-key`: Path to TLS private key file

## Key Learning Concepts

This project demonstrates several important Go web development concepts:

### 1. **HTTP Routing**
- Using `http.ServeMux` for request routing
- RESTful URL patterns
- Method-based routing

### 2. **Templating**
- Go's `html/template` package
- Template inheritance and composition
- Data passing between handlers and templates

### 3. **Database Integration**
- MySQL integration with `database/sql`
- Prepared statements for security
- Connection pooling and management

### 4. **Middleware**
- Request logging
- Panic recovery
- Security headers
- Authentication checks

### 5. **Security**
- HTTPS/TLS implementation
- Password hashing with bcrypt
- CSRF protection
- Secure session management
- Input validation and sanitization

### 6. **Error Handling**
- Custom error pages
- Centralized error handling
- Graceful error recovery

## API Endpoints

| Method | URL | Description |
|--------|-----|-------------|
| GET | `/` | Home page with recent snippets |
| GET | `/snippet/view/:id` | View a specific snippet |
| GET | `/snippet/create` | Show create snippet form |
| POST | `/snippet/create` | Create a new snippet |
| GET | `/user/signup` | Show user registration form |
| POST | `/user/signup` | Register a new user |
| GET | `/user/login` | Show login form |
| POST | `/user/login` | Authenticate user |
| POST | `/user/logout` | Log out user |
| GET | `/static/` | Serve static assets |

## Development

### File Structure Conventions

- **Handlers**: HTTP request handlers in `cmd/web/handlers.go`
- **Models**: Database models in `internal/models/`
- **Templates**: HTML templates in `ui/html/`
- **Static Files**: CSS, JS, images in `ui/static/`

### Adding New Features

1. Create the handler in `cmd/web/handlers.go`
2. Add the route in `cmd/web/routes.go`
3. Create necessary templates in `ui/html/`
4. Add any database models in `internal/models/`

## Testing

Run the test suite:

```bash
go test -v ./...
```

The application includes:
- Unit tests for handlers
- Integration tests for database operations
- End-to-end tests for key user flows

## Deployment

### Building for Production

```bash
go build -o snippetbox ./cmd/web
```

### Docker Deployment

```dockerfile
FROM golang:1.21-alpine AS builder
WORKDIR /app
COPY . .
RUN go build -o snippetbox ./cmd/web

FROM alpine:latest
RUN apk --no-cache add ca-certificates
WORKDIR /root/
COPY --from=builder /app/snippetbox .
COPY --from=builder /app/ui ./ui
COPY --from=builder /app/tls ./tls
CMD ["./snippetbox"]
```

## Contributing

This project is primarily for educational purposes, following the "Let's Go" book. However, contributions are welcome:

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

## Learning Resources

- **Book**: "Let's Go" by Alex Edwards - The primary resource this project follows
- **Go Documentation**: https://golang.org/doc/
- **Go Web Development**: https://golang.org/doc/articles/wiki/

## License

This project is created for educational purposes following the "Let's Go" book. Please refer to the book's licensing terms for commercial use.

## Acknowledgments

- Alex Edwards for the excellent "Let's Go" book
- The Go community for fantastic documentation and tools
- Contributors and fellow learners working through the same material

---

**Note**: This project is built step-by-step following the "Let's Go" book. Each chapter introduces new concepts and features, making it an excellent learning resource for Go web development.
