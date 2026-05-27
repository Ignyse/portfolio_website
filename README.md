# portfolio_website
Accessible at [ignacysus.com](www.ignacysus.com)

## Stack
- Svelte + SvelteKit 
- TailWind CSS 
- Vite
- Cloudflare -> DNS + Hosting

## run server
  1: cd portfolio                           │
│    2: npm run dev -- --open                  │
│                                              │
│  To close the dev server, hit Ctrl-C      

## using adapted static for deployment
(if issue conda deactivate, then nvm use 22)
npm i -D @sveltejs/adapter-static
npm i -D @sveltejs/adapter-cloudflare

added layout.js to prerender