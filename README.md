# Notification Service — Smart Campus Services

Notification microservice for the Smart Campus Services platform.

## Features

- **Send Notifications** — Triggered by Course and Timetable services
- **List & Filter** — By type, read status, with pagination
- **Mark as Read** — Individual or bulk
- **Stats Dashboard** — Notification counts by type
- **Delivery Callbacks** — Reports delivery status back to Course Service
- **Internal Auth** — Supports both JWT and API key for service-to-service calls

## API Endpoints

| Method | Endpoint                  | Auth    | Description                       |
| ------ | ------------------------- | ------- | --------------------------------- |
| GET    | `/notifications`          | JWT     | List notifications (filtered)     |
| GET    | `/notifications/stats`    | JWT     | Notification statistics           |
| GET    | `/notifications/:id`      | JWT     | Get by ID                         |
| POST   | `/notifications/send`     | JWT/Key | Send notification (inter-service) |
| PUT    | `/notifications/:id/read` | JWT     | Mark as read                      |
| PUT    | `/notifications/read-all` | JWT     | Mark all as read                  |
| DELETE | `/notifications/:id`      | JWT     | Delete notification               |
| GET    | `/health`                 | No      | Health check                      |

## Inter-Service Communication

1. **Course Service → Notification Service**: Sends enrollment confirmation notifications via `POST /notifications/send`
2. **Timetable Service → Notification Service**: Sends schedule reminders via `POST /notifications/send`
3. **Notification Service → Course Service**: Delivery status callback to Course Service after sending

## Quick Start

```bash
npm install
cp .env.example .env
npm run dev     # http://localhost:3004
```

## Testing

```bash
npm test
```

## Production Deployment

- **Deployed URL:** https://notification-service-e8ve.onrender.com
- **API Gateway URL:** [YOUR_API_GATEWAY_URL]

> For all production API calls, use the API Gateway URL above. Direct service URLs are for internal use and debugging only.

## CI/CD & Security

- Automated build, test, and deploy via GitHub Actions
- Static analysis: SonarCloud
- Dependency scanning: Snyk

---

## License

MIT
