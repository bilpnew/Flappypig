import type React from "react"
import type { Metadata } from "next"
import { Geist, Geist_Mono } from "next/font/google"
import "./globals.css"

const _geist = Geist({ subsets: ["latin"] })
const _geistMono = Geist_Mono({ subsets: ["latin"] })

export const metadata: Metadata = {
  title: "Flappy Pig - Fun Flying Game",
  description: "Help the adorable pig with wings fly through obstacles in this fun Flappy Bird-style game",
  generator: "v0.app",
  icons: {
    icon: [
      {
        url: "/icon-light-32x32.png",
        media: "(prefers-color-scheme: light)",
      },
      {
        url: "/icon-dark-32x32.png",
        media: "(prefers-color-scheme: dark)",
      },
      {
        url: "/icon.svg",
        type: "image/svg+xml",
      },
    ],
    apple: "/apple-icon.png",
  },
}

export default function RootLayout({
  children,
}: Readonly<{
  children: React.ReactNode
}>) {
  return (
    <html lang="en" suppressHydrationWarning>
      <head>
        <script
          dangerouslySetInnerHTML={{
            __html: `
              // Suppress errors from browser extensions and v0 infrastructure
              window.addEventListener('unhandledrejection', function(event) {
                const reason = event.reason?.message || event.reason?.toString() || '';
                // Suppress v0 ServiceWorker, MetaMask, and other external errors
                if (reason.includes('ServiceWorker') || 
                    reason.includes('__v0_sw') ||
                    reason.includes('MetaMask') || 
                    reason.includes('ethereum') ||
                    reason.includes('Worker disallowed')) {
                  event.preventDefault();
                  // Silent - don't log to keep console clean
                  return;
                }
              });
              
              window.addEventListener('error', function(event) {
                const message = event.message || '';
                if (message.includes('ServiceWorker') || 
                    message.includes('__v0_sw') ||
                    message.includes('MetaMask') || 
                    message.includes('ethereum') ||
                    message.includes('Worker disallowed')) {
                  event.preventDefault();
                  return;
                }
              });
            `,
          }}
        />
      </head>
      <body className={`font-sans antialiased`}>{children}</body>
    </html>
  )
}
