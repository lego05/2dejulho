"use client"

import { useState } from "react"
import Link from "next/link"
import Image from "next/image"
import { Menu, X, Phone } from "lucide-react"
import { Button } from "@/components/ui/button"

export default function Header() {
  const [isMenuOpen, setIsMenuOpen] = useState(false)

  const toggleMenu = () => {
    setIsMenuOpen(!isMenuOpen)
  }

  const closeMenu = () => {
    setIsMenuOpen(false)
  }

  const menuItems = [
    { name: "Home", href: "#home" },
    { name: "Serviços", href: "#servicos" },
    { name: "Contato", href: "#contato" },
    { name: "Pagamento", href: "#pagamento" },
    { name: "Depoimentos", href: "#depoimentos" },
  ]

  return (
    <header className="sticky top-0 z-50 bg-white shadow-md">
      <div className="container mx-auto px-4 md:px-6">
        <div className="flex items-center justify-between h-15 md:h-20">
          {/* Logo */}
          <div className="flex-shrink-0">
            <Link href="/" className="flex items-center">
              <Image
                src="/images/logo-2-de-julho.png"
                alt="2 de Julho - Guincho 24h"
                width={240}
                height={80}
                className="h-16 w-auto md:h-20"
              />
            </Link>
          </div>

          {/* Desktop Navigation */}
          <nav className="hidden md:flex space-x-8">
            {menuItems.map((item) => (
              <Link
                key={item.name}
                href={item.href}
                className="text-black hover:text-[#1e40af] font-medium transition-colors"
                onClick={closeMenu}
              >
                {item.name}
              </Link>
            ))}
          </nav>

          {/* Call Button */}
          <div className="hidden md:block">
            <Link
              href="tel:+5511996034000"
              className="inline-flex items-center justify-center gap-2 rounded-md bg-[#1e40af] px-4 py-2 text-white font-medium hover:bg-[#1e40af]/90 transition-colors"
            >
              <Phone className="h-4 w-4" />
              (11) 99603-4000
            </Link>
          </div>

          {/* Mobile Menu Button */}
          <div className="md:hidden">
            <Button
              variant="ghost"
              size="icon"
              onClick={toggleMenu}
              aria-label={isMenuOpen ? "Fechar menu" : "Abrir menu"}
            >
              {isMenuOpen ? <X className="h-6 w-6" /> : <Menu className="h-6 w-6" />}
            </Button>
          </div>
        </div>
      </div>

      {/* Mobile Navigation */}
      {isMenuOpen && (
        <div className="md:hidden bg-white border-t border-gray-300">
          <div className="container mx-auto px-4 py-3">
            <nav className="flex flex-col space-y-3">
              {menuItems.map((item) => (
                <Link
                  key={item.name}
                  href={item.href}
                  className="text-black hover:text-[#1e40af] py-2 font-medium transition-colors"
                  onClick={closeMenu}
                >
                  {item.name}
                </Link>
              ))}
              <Link
                href="tel:+5511996034000"
                className="inline-flex items-center justify-center gap-2 rounded-md bg-[#1e40af] px-4 py-2 text-white font-medium hover:bg-[#1e40af]/90 transition-colors w-full mt-2"
                onClick={closeMenu}
              >
                <Phone className="h-4 w-4" />
                Ligar Agora
              </Link>
            </nav>
          </div>
        </div>
      )}
    </header>
  )
}
