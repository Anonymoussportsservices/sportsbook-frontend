# sportsbook-frontend// Root files // README.md

Sportsbook Frontend (Next.js)

A basic frontend scaffold for a sportsbook platform built with Next.js and TailwindCSS. Ready for Vercel deployment.


---

Setup

npm install
npm run dev

Create a .env.local file from .env.example if needed.


---

// .env.example NEXT_PUBLIC_API_URL=https://your-api.com


---

// next.config.js /** @type {import('next').NextConfig} */ const nextConfig = { reactStrictMode: true, } module.exports = nextConfig;


---

// vercel.json { "rewrites": [ { "source": "/api/(.*)", "destination": "/api/$1" } ] }


---

// src/styles/globals.css @tailwind base; @tailwind components; @tailwind utilities;


---

// src/utils/api.ts export const api = { login: async (email: string, password: string) => { return await fetch(${process.env.NEXT_PUBLIC_API_URL}/login, { method: 'POST', headers: { 'Content-Type': 'application/json' }, body: JSON.stringify({ email, password }) }).then(res => res.json()); } };


---

// src/components/Layout.tsx import React from 'react';

const Layout = ({ children }: { children: React.ReactNode }) => (

  <div className="min-h-screen bg-gray-100 p-4">
    <div className="max-w-6xl mx-auto">{children}</div>
  </div>
);export default Layout;


---

// src/components/LoginForm.tsx import { useState } from 'react'; import { api } from '../utils/api';

export default function LoginForm() { const [email, setEmail] = useState(''); const [password, setPassword] = useState('');

const handleSubmit = async (e: React.FormEvent) => { e.preventDefault(); const result = await api.login(email, password); if (result?.token) { localStorage.setItem('token', result.token); alert('Logged in!'); } else { alert('Login failed'); } };

return ( <form onSubmit={handleSubmit} className="space-y-4 max-w-md mx-auto"> <input className="w-full p-2 border" placeholder="Email" value={email} onChange={e => setEmail(e.target.value)} /> <input className="w-full p-2 border" type="password" placeholder="Password" value={password} onChange={e => setPassword(e.target.value)} /> <button type="submit" className="w-full p-2 bg-blue-500 text-white">Login</button> </form> ); }


---

// src/components/OddsBoard.tsx export default function OddsBoard() { return ( <div className="p-4 bg-white shadow rounded">Odds Display Coming Soon</div> ); }


---

// src/components/BonusPanel.tsx export default function BonusPanel() { return ( <div className="p-4 bg-green-100 border border-green-400 rounded"> Inline bonus preview area </div> ); }


---

// src/pages/index.tsx import Layout from '../components/Layout'; import OddsBoard from '../components/OddsBoard';

export default function Home() { return ( <Layout> <h1 className="text-xl font-bold mb-4">Sportsbook Home</h1> <OddsBoard /> </Layout> ); }


---

// src/pages/login.tsx import Layout from '../components/Layout'; import LoginForm from '../components/LoginForm';

export default function LoginPage() { return ( <Layout> <h1 className="text-xl font-bold mb-4">Login</h1> <LoginForm /> </Layout> ); }


---

// src/pages/admin.tsx import Layout from '../components/Layout'; import BonusPanel from '../components/BonusPanel';

export default function AdminPage() { return ( <Layout> <h1 className="text-xl font-bold mb-4">Admin Dashboard</h1> <BonusPanel /> </Layout> ); }

