# [roomGPT.io](https://roomGPT.io)

This project generates new designs of your room with AI

[![Room GPT](./public/screenshot.png)](https://roomGPT.io)

## How it works

It uses an ML model called [ControlNet](https://github.com/lllyasviel/ControlNet) to generate variations of rooms. This application gives you the ability to upload a photo of any room, which will send it through this ML Model using a Next.js API route, and return your generated room. The ML Model is hosted on [Replicate](https://replicate.com) and [Upload](https://upload.io) is used for image storage. [Loops](https://loops.so/) is used for emails.

## Running Locally

### Cloning the repository the local machine.

```bash
git clone https://github.com/Nutlope/roomGPT
```

### Deploy a api server with model using Replicate's image. 

```bash
docker run -d -p 5000:5000 --gpus=all r8.im/jagilley/controlnet-hough@sha256:854e8727697a057c525cdb45ab037f64ecca770a1769cc52287c2e56472a247b
```
This image from the [jagilley/controlnet-hough](https://replicate.com/jagilley/controlnet-hough/api) pages

### Storing the API port in .env

Create a file in root directory of project with env. And store your API port in it, as shown in the .example.env file.

If you'd also like to do rate limiting, create an account on UpStash, create a Redis database, and populate the two environment variables in `.env` as well. If you don't want to do rate limiting, you don't need to make any changes.

### Installing the dependencies.

```bash
npm install
```

### Running the application.

Then, run the application in the command line and it will be available at `http://localhost:3000`.

```bash
npm run dev
```

## Auth setup

1. Use `openssl rand -base64 32` to generate NEXTAUTH_SECRET
2. Add DB URL and SHADOW DB URL from Neon
3. Create a new project in console.cloud.google.com
4. Click configure consent screen in API credentials page and click external
5. Add an app name, do not upload logo, add authorized domain
6. Publish app
7. Create credentials -> Oauth client ID
8. Run npx prisma db push && prisma migrate dev && prisma generate

## Todo
- [ ] Combine there service into a docker-compose.yml file