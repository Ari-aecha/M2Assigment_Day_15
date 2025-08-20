# Day 15 – Mongoose Validation and Schema Rules

This project demonstrates applying validation rules in Mongoose to ensure data integrity before saving to MongoDB.

## How to run

1. Install dependencies
   ```bash
   npm install
   ```

2. Copy `.env.example` to `.env` and set `MONGO_URI`

3. Start the server
   ```bash
   npm run dev
   ```

4. Test the API
   - `POST http://localhost:3000/api/add-student`
   - JSON body:
     ```json
     {
       "name": "Shifa A. Zafar",
       "email": "shifa@example.com",
       "course": "Computer Science"
     }
     ```

## Validation rules

- `name`: required, min length 3
- `email`: required, unique, must match basic email regex
- `course`: required

## Expected responses

### Success (201)
```json
{
  "message": "Student created",
  "data": { "...": "created document" }
}
```

### Validation error (400)
```json
{
  "message": "Validation failed",
  "errors": {
    "name": "name must be at least 3 characters"
  }
}
```

### Duplicate email (409)
```json
{
  "message": "Duplicate key error",
  "errors": {
    "email": "email must be unique"
  }
}
```

## Notes

- Unique email is enforced with a MongoDB unique index. Duplicate values trigger an `E11000 duplicate key` error, handled in `server.js` global error handler.
- All Mongoose validators run on `Model.create()` and `doc.save()`.
