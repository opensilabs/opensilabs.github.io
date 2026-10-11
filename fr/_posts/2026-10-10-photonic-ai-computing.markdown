---
lng_pair: id_20261010_photonic-ai-computing
title: "L'ordinateur fait de lumière"
author: OpenSI-Labs
category: chips
tags: [calcul photonique, réseaux de neurones optiques, efficacité énergétique, Université Koç, matériel]
date: 2026-10-10 06:00:00 -0700
img: /assets/img/posts/2026-10-10-photonic-ai-computing.png
meta_description: "Deux nouvelles études de l'Université Koç montrent le calcul d'IA se produisant dans la lumière elle-même : un réseau de neurones photonique qui préserve la couleur, et une cavité laser à fibre qui calcule avec sa propre physique."
---

Chaque modèle d'IA que vous avez utilisé a réfléchi avec des électrons : des milliards de transistors qui commutent, chacun brûlant un peu d'énergie et la rejetant en chaleur. La réponse de l'industrie a été de construire toujours plus grand — grappes plus vastes, contrats d'électricité plus gros, la consommation d'une petite ville pour répondre à vos questions.

Deux études récentes du laboratoire d'Uğur Teğin à l'Université Koç d'Istanbul posent une autre question : et si la réflexion se faisait dans des photons ? La lumière transporte plusieurs flux d'information à la fois, et son « calcul » se fait à la vitesse de son déplacement, pour ainsi dire gratuitement. L'une (*Communications Engineering*) construit un réseau de neurones photonique qui traite les images couleur sans jeter leur couleur ; l'autre (*Communications Physics*) transforme un laser à fibre en processeur à lui tout seul. [Couvertes ensemble cette semaine](https://techxplore.com/news/2026-10-approach-sustainable-ai-offloading-burden.html), elles dessinent une philosophie du matériel d'IA véritablement différente.

## Ne jetez pas la couleur

Commençons par un fait qui semble trivial jusqu'à ce qu'on en compte le coût : la plupart des classifieurs d'images commencent par jeter de l'information, écrasant les canaux rouge, vert et bleu en un seul canal de gris. Habitude d'une époque où le calcul était rare. Mais la couleur est un signal : le diagnostic d'une lésion cutanée peut tenir à une rougeur subtile ; le sens d'une image satellite peut résider dans le vert.

Le système de Kılınç et Teğin refuse ce raccourci. L'image est encodée sur un dispositif programmable qui façonne la propagation de la lumière : un empilement de masques de phase (conversion multi-plans) mélange et transforme les trois canaux pendant qu'ils traversent ensemble l'optique, accentuant physiquement les traits qui distinguent une image d'une autre — couleur, forme, texture. Une caméra enregistre le motif obtenu, et un classifieur en lit la catégorie.

Les chiffres sont frappants : en dermatologie, la précision passe de 68 % sur pixels bruts à **98 %** après prétraitement optique. Sur l'imagerie médicale, les images naturelles et la régression, l'optique ajoute 25 à 45 points par rapport aux pixels bruts ; garder le RVB au lieu du gris vaut à lui seul 6 à 11 points ([article](https://www.nature.com/articles/s44172-026-00762-w)).

<svg viewBox="0 0 720 470" width="100%" style="max-width:720px;display:block;margin:1.2em auto;" role="img" aria-label="Pipeline de calcul optique multicanal : les trois canaux RVB encodés sur des masques de phase, transformés par la propagation de la lumière, lus par une caméra">
  <defs>
    <marker id="arrP" markerWidth="9" markerHeight="9" refX="7" refY="4.5" orient="auto"><path d="M0,0 L9,4.5 L0,9 Z" fill="#1c7ed6"/></marker>
  </defs>
  <text x="360" y="24" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="15" font-weight="700" fill="#212529">Calcul optique multicanal : la couleur survit à tout le pipeline</text>
  <rect x="30" y="50" width="150" height="70" rx="10" fill="#fff5f5" stroke="#c92a2a" stroke-width="2"/>
  <text x="105" y="76" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="13" font-weight="700" fill="#a61e4d">IMAGE RVB</text>
  <text x="105" y="96" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="12" fill="#495057">les 3 canaux conservés</text>
  <rect x="30" y="140" width="150" height="26" rx="6" fill="#f8f9fa" stroke="#adb5bd"/>
  <text x="105" y="157" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="11" fill="#495057">pas de passage au gris</text>
  <line x1="180" y1="85" x2="225" y2="85" stroke="#1c7ed6" stroke-width="2" marker-end="url(#arrP)"/>
  <rect x="225" y="50" width="170" height="70" rx="10" fill="#e7f5ff" stroke="#1c7ed6" stroke-width="2"/>
  <text x="310" y="76" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="13" font-weight="700" fill="#1864ab">MASQUES DE PHASE</text>
  <text x="310" y="96" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="12" fill="#495057">conversion multi-plans</text>
  <line x1="395" y1="85" x2="440" y2="85" stroke="#1c7ed6" stroke-width="2" marker-end="url(#arrP)"/>
  <rect x="440" y="50" width="150" height="70" rx="10" fill="#fff3bf" stroke="#f08c00" stroke-width="2"/>
  <text x="515" y="76" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="13" font-weight="700" fill="#e67700">PROPAGATION</text>
  <text x="515" y="96" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="12" fill="#495057">traits accentués optiquement</text>
  <line x1="590" y1="85" x2="620" y2="85" stroke="#1c7ed6" stroke-width="2" marker-end="url(#arrP)"/>
  <rect x="620" y="50" width="80" height="70" rx="10" fill="#f3f0ff" stroke="#7048e8" stroke-width="2"/>
  <text x="660" y="76" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="12" font-weight="700" fill="#5f3dc4">CAMÉRA</text>
  <text x="660" y="96" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="11" fill="#495057">+ classifieur</text>
  <rect x="120" y="200" width="480" height="120" rx="10" fill="#ebfbee" stroke="#2b8a3e" stroke-width="2"/>
  <text x="360" y="228" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="14" font-weight="700" fill="#2b8a3e">BOUCLE D'AUTO-OPTIMISATION</text>
  <text x="360" y="252" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="12" fill="#495057">apprend des mesures expérimentales — aucun simulateur parfait requis</text>
  <text x="360" y="274" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="12" fill="#495057">optimisation bayésienne (mélange des canaux) + matériel en boucle</text>
  <text x="360" y="296" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="12" fill="#495057">criticalité auto-organisée (phases) — s'adapte aux désalignements</text>
  <line x1="310" y1="120" x2="310" y2="195" stroke="#2b8a3e" stroke-width="2" stroke-dasharray="6,4" marker-end="url(#arrP)"/>
  <rect x="225" y="350" width="270" height="70" rx="10" fill="#ffffff" stroke="#212529" stroke-width="2"/>
  <text x="360" y="378" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="14" font-weight="700" fill="#212529">DERMATOLOGIE : 68 % → 98 %</text>
  <text x="360" y="400" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="12" fill="#495057">l'auto-optimisation ajoute 7 à 12 points</text>
  <text x="360" y="448" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="11" fill="#868e96">Légende : les canaux RVB traversent ensemble des masques de phase programmables ; le système se règle sur le matériel réel.</text>
</svg>

## Apprendre le dispositif, pas la simulation

Voici le point qui compte le plus, et ce n'est pas la précision. Les réseaux de neurones optiques ont un problème de cimetière : merveilleux en simulation, morts au laboratoire. Désalignements, imperfections de fabrication, dérives thermiques — le dispositif physique ne correspond jamais au modèle idéalisé, et l'écart dévore la performance.

L'équipe de Teğin a inversé le problème : au lieu d'exiger un simulateur parfait, le système apprend des mesures expérimentales. Deux stratégies complémentaires fonctionnent sans modèle direct différentiable : l'optimisation bayésienne affine le mélange des canaux à l'entrée, et un protocole matériel-en-boucle fondé sur la criticalité auto-organisée explore les réglages de phase en grande dimension. La machine apprend les petites manies de son matériel et s'y adapte — les imperfections ne sont pas un bruit à éliminer, elles font partie de ce qui est appris. Gain supplémentaire : 7 à 12 points.

L'électronique a passé soixante ans à exiger des tolérances toujours plus serrées — nanomètres, aujourd'hui angströms. Le pari inverse : construire l'ordinateur avec une physique imparfaite, puis laisser la physique enseigner l'algorithme. Une philosophie du matériel véritablement différente — et la raison pour laquelle ce travail mérite l'attention au-delà du tableau des scores.

## Un laser qui pense

La seconde étude est plus étrange, et d'une certaine façon plus radicale. Eşlik, Kesgin, Kılınç et Teğin ont pris un laser à fibre multimode en onde continue — une bobine de fibre qui amplifie la lumière — et utilisé la cavité elle-même comme processeur. Les images sont écrites comme motifs de phase sur un modulateur spatial de lumière ; la lumière circule dans la cavité, où l'interférence multimode et la saturation du gain — le comportement physique propre du laser — la brassent en une transformation non linéaire de grande dimension. Il en émerge un motif d'intensité stable aux classes déjà séparées : un simple classifieur linéaire termine le travail.

Aucun GPU n'a effectué la transformation non linéaire — la physique s'en est chargée. Sur déchets recyclables, images météo et satellite, scans de rétine et lésions cutanées : **85 à 99 %** de précision avec des ordres de grandeur de paramètres en moins qu'un réseau profond classique ([article](https://www.nature.com/articles/s42005-026-02823-0)).

<svg viewBox="0 0 720 400" width="100%" style="max-width:720px;display:block;margin:1.2em auto;" role="img" aria-label="La cavité laser à fibre comme processeur optique non linéaire : des images encodées en phase transformées par la dynamique du laser en motifs séparables">
  <defs>
    <marker id="arrQ" markerWidth="9" markerHeight="9" refX="7" refY="4.5" orient="auto"><path d="M0,0 L9,4.5 L0,9 Z" fill="#1c7ed6"/></marker>
  </defs>
  <text x="360" y="24" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="15" font-weight="700" fill="#212529">La cavité laser est le processeur</text>
  <rect x="20" y="60" width="130" height="70" rx="10" fill="#fff5f5" stroke="#c92a2a" stroke-width="2"/>
  <text x="85" y="88" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="13" font-weight="700" fill="#a61e4d">IMAGE</text>
  <text x="85" y="108" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="12" fill="#495057">déchets, satellite, rétine…</text>
  <line x1="150" y1="95" x2="190" y2="95" stroke="#1c7ed6" stroke-width="2" marker-end="url(#arrQ)"/>
  <rect x="190" y="60" width="140" height="70" rx="10" fill="#e7f5ff" stroke="#1c7ed6" stroke-width="2"/>
  <text x="260" y="88" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="13" font-weight="700" fill="#1864ab">MODULATEUR</text>
  <text x="260" y="108" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="12" fill="#495057">encodage en phase</text>
  <line x1="330" y1="95" x2="370" y2="95" stroke="#1c7ed6" stroke-width="2" marker-end="url(#arrQ)"/>
  <rect x="370" y="50" width="200" height="90" rx="40" fill="#fff3bf" stroke="#f08c00" stroke-width="2"/>
  <text x="470" y="80" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="13" font-weight="700" fill="#e67700">CAVITÉ LASER À FIBRE</text>
  <text x="470" y="100" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="12" fill="#495057">interférence multimode</text>
  <text x="470" y="118" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="12" fill="#495057">+ saturation du gain</text>
  <line x1="570" y1="95" x2="610" y2="95" stroke="#1c7ed6" stroke-width="2" marker-end="url(#arrQ)"/>
  <rect x="610" y="60" width="90" height="70" rx="10" fill="#f3f0ff" stroke="#7048e8" stroke-width="2"/>
  <text x="655" y="88" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="12" font-weight="700" fill="#5f3dc4">CLASSI-</text>
  <text x="655" y="106" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="12" font-weight="700" fill="#5f3dc4">FIEUR</text>
  <rect x="190" y="180" width="380" height="80" rx="10" fill="#ffffff" stroke="#212529" stroke-width="2"/>
  <text x="380" y="210" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="14" font-weight="700" fill="#212529">PRÉCISION DE 85 À 99 %</text>
  <text x="380" y="232" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="12" fill="#495057">des ordres de grandeur de paramètres en moins qu'un réseau profond</text>
  <text x="380" y="252" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="12" fill="#495057">— la dynamique du laser remplace les couches cachées</text>
  <text x="360" y="310" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="13" font-weight="700" fill="#212529">Pourquoi ça marche : la non-linéarité est gratuite</text>
  <text x="360" y="334" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="12" fill="#495057">Dans un réseau numérique, la non-linéarité coûte multiplications matricielles et trafic mémoire.</text>
  <text x="360" y="354" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="12" fill="#495057">Dans la cavité, c'est simplement ce que fait la lumière en traversant.</text>
  <text x="360" y="386" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="11" fill="#868e96">Légende : les images deviennent des motifs de phase ; la dynamique du laser effectue le calcul non linéaire.</text>
</svg>

## Le compte, honnêtement

Deux réserves, car ce journal ne fait pas dans l'exagération. D'abord, aucun des deux systèmes n'est pure lumière : écrire les données exige des modulateurs spatiaux, lire les motifs des caméras, optimiser des unités de contrôle. La vraie question est la fraction de la charge totale que la lumière peut absorber — aujourd'hui le gros du milieu, la transformation non linéaire, tandis que les bords restent électroniques. Des modulateurs plus rapides et une photonique intégrée sur puce pourront-ils pousser cette fraction vers tout le pipeline ? C'est le pari d'ingénierie ouvert.

Ensuite, ce sont des preuves de concept, pas des remplaçants de centres de données — personne n'entraînera un modèle de pointe dans un laser à fibre l'an prochain.

Mais la direction est bonne, et le moment compte. L'inférence bute sur des limites physiques — puissance, chaleur, va-et-vient des données entre mémoire et processeurs. Chacune est une propriété de l'électronique. Le calcul photonique ne les contourne pas seulement : il inverse la plus dure. Là où l'électronique exige la perfection et la paie au prix de la fabrication, la photonique apprend le dispositif qu'elle a sous la main. Calculer *avec* la physique au lieu de lutter contre elle.

Les années 1980 rêvaient d'ordinateurs optiques et ont échoué sur la programmabilité et l'adaptativité. La pièce manquante, semble-t-il, n'était pas une meilleure optique. C'était de laisser l'optique s'enseigner elle-même.

**Discussion :** si le matériel d'IA de demain apprend les imperfections de son propre substrat physique au lieu d'exiger une fabrication parfaite, que devient l'économie de la fabrication des puces — et qui gagne quand une « physique assez bonne » bat le silicium parfait ?
