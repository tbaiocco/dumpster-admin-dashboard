# Dumpster Admin Dashboard

Administrative interface for managing the Dumpster application - a universal life inbox that captures, categorizes, and retrieves information from emails and other sources.

## Tech Stack

- **React 19.2.0** - UI framework
- **TypeScript 4.9.5** - Type safety
- **React Scripts 5.0.1** - Build tooling (Create React App)
- **Tailwind CSS** - Styling
- **shadcn/ui** - Component library
- **React Router 7.9.5** - Routing
- **Axios** - API communication
- **Recharts** - Analytics visualization

## Quick Start

## Available Scripts

In the project directory, you can run:

### `npm start`

Runs the app in the development mode.\
Open [http://localhost:3000](http://localhost:3000) to view it in the browser.

The page will reload if you make edits.\
You will also see any lint errors in the console.

### `npm test`

Launches the test runner in the interactive watch mode.\
See the section about [running tests](https://facebook.github.io/create-react-app/docs/running-tests) for more information.

### `npm run build`

Builds the app for production to the `build` folder.\
It correctly bundles React in production mode and optimizes the build for the best performance.

The build is minified and the filenames include the hashes.\
Your app is ready to be deployed!

## Environment Variables

Create a `.env.local` file for local development:

```env
VITE_API_URL=http://localhost:3000
```

For production (Railway), set in the Railway dashboard:
```env
VITE_API_URL=https://your-backend.railway.app
```

## Deployment

### Railway (Recommended)

See [RAILWAY_DEPLOY.md](./RAILWAY_DEPLOY.md) for complete deployment instructions.

Quick deploy:
1. Push to GitHub
2. Connect repository to Railway
3. Set `VITE_API_URL` environment variable
4. Deploy automatically

### Docker

Production build with Nginx:
```bash
docker build -f Dockerfile.prod -t admin-dashboard .
docker run -p 80:80 admin-dashboard
```

## Project Structure

```
src/
├── components/     # Reusable UI components
├── pages/         # Page components with routing
├── services/      # API service layer
└── lib/           # Utilities and helpers
```

## Learn More

- [Create React App documentation](https://facebook.github.io/create-react-app/docs/getting-started)
- [React documentation](https://react.dev)
- [Railway deployment guide](./RAILWAY_DEPLOY.md)

If you aren’t satisfied with the build tool and configuration choices, you can `eject` at any time. This command will remove the single build dependency from your project.

Instead, it will copy all the configuration files and the transitive dependencies (webpack, Babel, ESLint, etc) right into your project so you have full control over them. All of the commands except `eject` will still work, but they will point to the copied scripts so you can tweak them. At this point you’re on your own.

You don’t have to ever use `eject`. The curated feature set is suitable for small and middle deployments, and you shouldn’t feel obligated to use this feature. However we understand that this tool wouldn’t be useful if you couldn’t customize it when you are ready for it.

## Learn More

You can learn more in the [Create React App documentation](https://facebook.github.io/create-react-app/docs/getting-started).

To learn React, check out the [React documentation](https://reactjs.org/).
