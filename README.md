import { Card, CardContent } from "@/components/ui/card";
import { Button } from "@/components/ui/button";
import { motion } from "framer-motion";
import { useState } from "react";

const products = [
  { name: "Fruits rouges", description: "Hydromel doux et acidulé aux fruits rouges.", image: "/fruits-rouges.jpg" },
  { name: "Mangue", description: "Saveur exotique et ensoleillée.", image: "/mangue.jpg" },
  { name: "Pomme", description: "Hydromel fruité et rafraîchissant.", image: "/pomme.jpg" },
  { name: "Poire", description: "Goût délicat et subtil de poire mûre.", image: "/poire.jpg" },
];

export default function Home() {
  const [selected, setSelected] = useState("Histoire");

  const sections = {
    Histoire: (
      <div className="space-y-4">
        <h2 className="text-2xl font-semibold">Notre histoire</h2>
        <p>
          MELO est née de la passion de trois amis pour l’hydromel artisanal. Fondée en 2020, notre entreprise met à l’honneur des recettes naturelles, inspirées des traditions nordiques. Nos salariés partagent la même envie : faire découvrir un breuvage ancestral, réinventé avec des arômes modernes.
        </p>
      </div>
    ),
    Produits: (
      <div className="grid grid-cols-1 md:grid-cols-2 gap-4">
        {products.map((p) => (
          <Card key={p.name} className="rounded-2xl shadow-md">
            <CardContent className="p-4">
              <img src={p.image} alt={p.name} className="w-full h-48 object-cover rounded-xl mb-2" />
              <h3 className="text-xl font-bold">{p.name}</h3>
              <p>{p.description}</p>
            </CardContent>
          </Card>
        ))}
      </div>
    ),
    Engagements: (
      <div className="space-y-4">
        <h2 className="text-2xl font-semibold">Nos engagements</h2>
        <ul className="list-disc pl-5 space-y-2">
          <li>Ingrédients 100% naturels et locaux</li>
          <li>Production respectueuse de l’environnement</li>
          <li>Bouteilles recyclables</li>
          <li>Soutien aux apiculteurs français</li>
        </ul>
      </div>
    ),
    Fabrication: (
      <div className="space-y-4">
        <h2 className="text-2xl font-semibold">Processus de fabrication</h2>
        <p>
          Notre hydromel est conçu à partir de miel pur, d’eau de source, et de fruits soigneusement sélectionnés. La fermentation naturelle dure plusieurs semaines pour garantir un goût subtil. Chaque arôme est infusé à froid pour conserver toute sa fraîcheur.
        </p>
      </div>
    ),
  };

  return (
    <main className="max-w-4xl mx-auto p-6 space-y-8">
      <header className="text-center">
        <motion.h1 className="text-4xl font-bold" initial={{ opacity: 0 }} animate={{ opacity: 1 }}>
          MELO — Hydromel Aromatisé
        </motion.h1>
        <p className="text-muted-foreground mt-2">L’élégance d’un nectar millénaire, réinventé.</p>
      </header>

      <nav className="flex justify-center gap-4 flex-wrap">
        {Object.keys(sections).map((key) => (
          <Button key={key} variant={selected === key ? "default" : "outline"} onClick={() => setSelected(key)}>
            {key}
          </Button>
        ))}
      </nav>

      <section className="min-h-[300px]">
        <motion.div
          key={selected}
          initial={{ opacity: 0, y: 10 }}
          animate={{ opacity: 1, y: 0 }}
          transition={{ duration: 0.3 }}
        >
          {sections[selected]}
        </motion.div>
      </section>
    </main>
  );
}

