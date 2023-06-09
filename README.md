# Express Route

Auto register handlers for Express, inspired by NextJS. 

Supported:
- Basic methods: GET, POST, PATH, OPTIONS, DELETE
- Middleware using _middleware
- Nested routes


### Example folder structure
```
├── src
│   ├── handlers
│   │   ├── _middleware.ts
│   │   ├── index.ts
│   │   │── index.post.ts
│   │   │── users
│   │       ├── index.ts
├── app.ts
```

### Register middleware
```ts
// src/handlers/_middleware.ts
import { Request, Response, NextFunction } from "express";

export default function(req: Request, res: Response, next: NextFunction) {
  console.log("/admin/_middleware");
  next()
}
```

### Register GET

```ts
// src/handlers/index.ts (or src/handlers/index.get.ts)
import { Request, Response } from "express";

export default function(req: Request, res: Response) {

  res.json({
    message: "ok"
  })
}
```

### Register nested route

```ts
// src/handlers/users/index.ts (or src/handlers/users.get.ts)
import { Request, Response } from "express";

export default function(req: Request, res: Response) {

  res.json({
    message: "ok"
  })
}
```

### Register routes

```ts
// app.ts
import path from "path"
import express from "express";
import register from "express-route-register";

const app = express();

register({
  app,
  // debug: true, // log registed handlers
  routePath: "/",
  dirPath: path.join(__dirname, "/handlers"),
});


const host = process.env.HOST || "localhost";
const port = parseInt(process.env.PORT || "8080");

app.listen(port, host, () => {
  console.log(`Server started ${host}:${port}`);
})
```