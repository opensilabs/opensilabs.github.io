---
lng_pair: id_20261015_pingpongduo-table-tennis
title: "PingpongDuo : deux humanoïdes, une table, zéro collision"
author: OpenSI-Labs
category: robotics
tags: [robots humanoïdes, tennis de table, coordination multi-robots, apprentissage par renforcement, PingpongDuo]
date: 2026-10-15 00:00:00 -0700
img: /assets/img/posts/2026-10-15-pingpongduo-table-tennis.png
meta_description: "PingpongDuo apprend à deux robots humanoïdes à jouer au tennis de table en double : alternance stricte, espace partagé, aucune collision, avec 13,2 % de retours réussis en plus et plus de 10 frappes alternées sur du vrai matériel."
---

**Le robot pongiste, c'est du passé. Le robot pongiste en double, c'est un autre sport.**

Un humanoïde qui renvoie une balle de ping-pong, c'est devenu une démo de routine. Le bras de DeepMind jouait déjà en compétition en 2024, l'Ace de Sony a affronté des professionnels pour un article dans *Nature*, le HITTER de Berkeley a enchaîné 106 frappes consécutives contre un humain ([HITTER, arXiv:2508.21043](https://arxiv.org/pdf/2508.21043)), et le SMASH de HKU l'a fait avec la seule vision embarquée ([arXiv:2604.01158](https://arxiv.org/html/2604.01158v1)). Mais le double — deux joueurs du même côté, obligés de frapper en alternance stricte, partageant quelques mètres carrés — met tous ces systèmes en échec. Votre partenaire est un obstacle mobile à ne jamais percuter, et dès que vous frappez, il faut lui libérer la place.

Un article publié le 14 octobre s'attaque au double de front ([Jiang et al., arXiv:2610.20579](https://arxiv.org/abs/2610.20579v1)). PingpongDuo est un cadre hiérarchique pour le double humanoïde agile avec coordination d'équipe sûre, et le premier système à faire échanger deux humanoïdes complets en alternance sur du vrai matériel.

L'architecture découpe le problème comme le ferait un entraîneur. Au niveau de l'équipe, un planificateur choisit conjointement les positions cibles des deux robots et soumet chaque proposition à des estimations de risque apprises qui filtrent les dangereuses — en préservant en priorité l'espace du frappeur actuel, pour que le robot qui s'apprête à frapper n'ait jamais à négocier sa place en plein geste. Au niveau individuel, le jeu de jambes et la frappe sont deux compétences apprises séparément : des jambes agiles pour se placer, un contrôle de raquette précis pour conclure. Les compétences s'appuient sur des références de mouvements humains, dont des jeux de jambes capturés lors de vrais matchs de double, et — la touche élégante — chaque compétence s'entraîne à partir d'états produits par l'autre, de sorte que le jeu de jambes apprend à finir exactement là où la frappe peut commencer.

<figure>
<svg viewBox="0 0 680 340" xmlns="http://www.w3.org/2000/svg" style="max-width:100%;height:auto;font-family:system-ui,sans-serif">
<text x="340" y="28" font-size="17" font-weight="bold" text-anchor="middle">Le double est un problème de relais : frapper, dégager, frapper</text>
<rect x="20" y="60" width="150" height="120" rx="10" fill="#eef4ff" stroke="#3366cc" stroke-width="1.5"/>
<text x="95" y="88" font-size="14" font-weight="bold" text-anchor="middle">Robot A frappe</text>
<text x="95" y="112" font-size="14" text-anchor="middle">le bras résiduel</text>
<text x="95" y="132" font-size="14" text-anchor="middle">affine le coup</text>
<text x="95" y="156" font-size="14" text-anchor="middle" font-style="italic">après le déplacement</text>
<rect x="200" y="60" width="150" height="120" rx="10" fill="#fff8ee" stroke="#cc8833" stroke-width="1.5"/>
<text x="275" y="88" font-size="14" font-weight="bold" text-anchor="middle">Robot A dégage</text>
<text x="275" y="112" font-size="14" text-anchor="middle">2,15 m en 2,4 s,</text>
<text x="275" y="132" font-size="14" text-anchor="middle">pointe à 2,23 m/s</text>
<text x="275" y="156" font-size="14" text-anchor="middle">erreur ~2 cm</text>
<rect x="380" y="60" width="150" height="120" rx="10" fill="#eef4ff" stroke="#3366cc" stroke-width="1.5"/>
<text x="455" y="88" font-size="14" font-weight="bold" text-anchor="middle">Robot B se place</text>
<text x="455" y="112" font-size="14" text-anchor="middle">le planificateur filtre</text>
<text x="455" y="132" font-size="14" text-anchor="middle">les cibles risquées,</text>
<text x="455" y="156" font-size="14" text-anchor="middle">garde l'espace du frappeur</text>
<rect x="560" y="60" width="100" height="120" rx="10" fill="#eefbf1" stroke="#339966" stroke-width="1.5"/>
<text x="610" y="88" font-size="14" font-weight="bold" text-anchor="middle">Robot B</text>
<text x="610" y="112" font-size="14" font-weight="bold" text-anchor="middle">frappe</text>
<text x="610" y="140" font-size="14" text-anchor="middle">→ boucle</text>
<line x1="170" y1="120" x2="196" y2="120" stroke="#555" stroke-width="2" marker-end="url(#p1)"/>
<line x1="350" y1="120" x2="376" y2="120" stroke="#555" stroke-width="2" marker-end="url(#p1)"/>
<line x1="530" y1="120" x2="556" y2="120" stroke="#555" stroke-width="2" marker-end="url(#p1)"/>
<path d="M 610 180 C 610 280, 95 280, 95 184" fill="none" stroke="#339966" stroke-width="2" stroke-dasharray="7,5" marker-end="url(#p1)"/>
<text x="340" y="262" font-size="14" text-anchor="middle">alternance stricte : chaque frappe rend la table au partenaire</text>
<text x="340" y="292" font-size="14" text-anchor="middle">jambes et frappe entraînés à partir des états de l'autre</text>
<text x="340" y="318" font-size="14" text-anchor="middle" font-style="italic">simulateur calibré sur des mesures réelles de vol et de contact</text>
<defs><marker id="p1" markerWidth="10" markerHeight="8" refX="9" refY="4" orient="auto"><path d="M0,0 L10,4 L0,8 z" fill="#555"/></marker></defs>
</svg>
<figcaption>Un échange complet : frapper, libérer l'espace, placer le partenaire, frapper à nouveau — le planificateur gardant l'espace du frappeur.</figcaption>
</figure>

Vient ensuite le pont entre simulation et réel, d'une honnêteté d'ingénieur rare. Une politique résiduelle du bras-raquette affine chaque frappe après le déplacement, à partir du retour d'un simulateur calibré avec des mesures réelles de vol de balle et de contact — pas un moteur physique générique, mais un simulateur réglé sur la façon dont cette balle vole et rebondit vraiment. En simulation, PingpongDuo bat le taux de retours réussis de la meilleure référence de 13,2 %. Sur de vrais robots, les chiffres ressemblent à une fiche d'athlète : un cycle dégagement-récupération de 2,15 mètres bouclé en 2,4 secondes, une vitesse de pointe de 2,23 mètres par seconde, une erreur de positionnement d'environ 2 centimètres pendant le dégagement — et deux robots qui enchaînent plus de 10 frappes consécutives en alternance stricte ([résumé ArXivSignals](https://arxivsignals.io/explore)).

<figure>
<svg viewBox="0 0 680 280" xmlns="http://www.w3.org/2000/svg" style="max-width:100%;height:auto;font-family:system-ui,sans-serif">
<text x="340" y="28" font-size="17" font-weight="bold" text-anchor="middle">Mesuré sur du vrai matériel, pas seulement en simulation</text>
<text x="230" y="72" font-size="14" text-anchor="end">Retours réussis (sim)</text>
<rect x="240" y="56" width="300" height="24" rx="4" fill="#3366cc"/><text x="548" y="73" font-size="14">+13,2 % vs meilleure réf.</text>
<text x="230" y="118" font-size="14" text-anchor="end">Dégagement + retour</text>
<rect x="240" y="102" width="200" height="24" rx="4" fill="#cc8833"/><text x="448" y="119" font-size="14">2,15 m en 2,4 s</text>
<text x="230" y="164" font-size="14" text-anchor="end">Vitesse de pointe</text>
<rect x="240" y="148" width="230" height="24" rx="4" fill="#cc8833"/><text x="478" y="165" font-size="14">2,23 m/s</text>
<text x="230" y="210" font-size="14" text-anchor="end">Échange alterné (réel)</text>
<rect x="240" y="194" width="260" height="24" rx="4" fill="#339966"/><text x="508" y="211" font-size="14">10+ frappes, alternance stricte</text>
<text x="340" y="254" font-size="14" text-anchor="middle" font-style="italic">erreur de positionnement pendant le dégagement : environ 2 cm</text>
</svg>
<figcaption>Les gains en simulation plus l'athlétisme réel : le sprint de dégagement est la compétence propre au double que les systèmes de simple n'ont jamais eue.</figcaption>
</figure>

Voici l'angle que la plupart des couvertures manqueront. Le double, c'est le moment où le travail d'équipe multi-robots cesse d'être une abstraction de planification pour devenir un problème de physique. Dans la plupart des recherches sur les « équipes de robots », la coordination signifie se répartir les tâches ou se relayer dans le logiciel. Ici, le coéquipier est un obstacle mobile de 50 kilos dans votre rayon de frappe, la balle file à plusieurs mètres par seconde, et le passage de relais entre « mon tour » et « ton tour » est un sprint corps entier. Le filtre de risque appris est la contribution conceptuelle : au lieu de planifier les deux robots conjointement en croisant les doigts, le système traite l'espace de travail du frappeur comme sacré et met son veto à tout ce qui le menace. La sécurité n'est pas une contrainte boulonnée après coup ; c'est le premier travail du planificateur.

Les réserves honnêtes : dix frappes alternées, c'est un échange, pas un match. L'article ne rapporte ni adversaires retors, ni effets violents, ni bruit de salle — le chaos du vrai jeu n'est pas encore au rendez-vous. Et comme tout athlète entraîné en simulation, le système ne vaut que son simulateur calibré.

La direction reste limpide. Le simple a prouvé que les robots peuvent être des athlètes. Le double prouve qu'ils peuvent être des coéquipiers — prédire le mouvement d'un partenaire, céder l'espace, arriver exactement là où la compétence suivante en a besoin. La table est petite, la balle est rapide, et pour la première fois, les robots ne jouent plus seuls.

Quand deux robots apprennent à partager une table sans se percuter — que se passe-t-il quand le coéquipier à prédire est un humain ?
