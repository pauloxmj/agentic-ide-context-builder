---
name: api-design
description: REST API design best practices and conventions. Use when creating or modifying API endpoints, when the user asks about API design, or when reviewing API code.
---

# API Design Guidelines

When designing or reviewing REST APIs, follow these conventions.

## URL Structure

- Use plural nouns for resources: `/users`, `/orders`
- Use kebab-case for multi-word resources: `/order-items`
- Nest related resources: `/users/{id}/orders`
- Maximum nesting depth: 2 levels
- Use query parameters for filtering, sorting, and pagination

## HTTP Methods

| Method | Purpose | Idempotent |
|--------|---------|------------|
| GET | Retrieve resources | ✅ |
| POST | Create new resources | ❌ |
| PUT | Replace entire resource | ✅ |
| PATCH | Partial update | ❌ |
| DELETE | Remove resource | ✅ |

## Response Format

All responses must follow this structure:

```json
{
  "data": {},
  "meta": { "page": 1, "totalPages": 10 },
  "errors": []
}
```

## Error Response Format

```json
{
  "error": {
    "code": "VALIDATION_ERROR",
    "message": "Human-readable description",
    "details": [
      { "field": "email", "message": "Invalid email format" }
    ]
  }
}
```

## Response Codes

| Code | When to Use |
|------|-------------|
| 200 | Successful GET, PUT, PATCH, DELETE |
| 201 | Successful POST (resource created) |
| 204 | Successful operation with no response body |
| 400 | Client error — bad request / validation failure |
| 401 | Authentication required |
| 403 | Authenticated but not authorized |
| 404 | Resource not found |
| 409 | Conflict (e.g., duplicate creation) |
| 422 | Unprocessable entity |
| 500 | Server error (should never be intentional) |

## Pagination

- Use `page` and `limit` query parameters
- Default `limit`: 20, maximum: 100
- Include pagination metadata in response

## Versioning

- Use URL path versioning: `/api/v1/users`
- Never remove fields from a response in the same version
- Document breaking changes clearly

## Standards

- Use ISO 8601 for dates: `2024-01-15T10:30:00Z`
- Use UUID for resource identifiers
- Always include `Content-Type: application/json` header
- Support `Accept-Language` for internationalized responses
