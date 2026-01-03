# Flappypig
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
              // Suppress errors from browser extensions (MetaMask, etc.)
              window.addEventListener('unhandledrejection', function(event) {
                // Check if error is from MetaMask or ServiceWorker
                const reason = event.reason?.message || event.reason?.toString() || '';
                if (reason.includes('MetaMask') || 
                    reason.includes('ServiceWorker') ||
                    reason.includes('ethereum')) {
                  event.preventDefault();
                  console.log('Suppressed external error:', reason);
                }
              });
              
              window.addEventListener('error', function(event) {
                const message = event.message || '';
                if (message.includes('MetaMask') || 
                    message.includes('ServiceWorker') ||
                    message.includes('ethereum')) {
                  event.preventDefault();
                  console.log('Suppressed external error:', message);
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
