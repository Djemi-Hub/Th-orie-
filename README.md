Choisir un domaine de votre choix
Posez 10 questions auxquelles vous souhaitez répondre avec votre graphe de connaissances.
Identifier les types de nœuds et de relations de votre graphe.
Créer votre graphe en utilisant la définition étendue de graphe multi-relationnel.
Vérifier que votre graphe répond aux 10 questions posées plus haut.  


import networkx as nx
import matplotlib.pyplot as plt

# Création du graphe
G = nx.DiGraph()

# Ajout des entités principales
entities = [
    "University1", "University2",
    "Faculté des Lettres Modernes", "Faculté d'Informatique", "Faculté SEA",
    "Teacher1", "Teacher2",
    "Student1", "Student2",
    "Session Course1", "Session Course2",
    "City1", "City2",
    "Cameroun", "Burkina Faso",
    "Afrique"
]

# Ajouter les noeuds
G.add_nodes_from(entities)

# Relations Facultés -> Universités
G.add_edge("Faculté des Lettres Modernes", "University1", label="belongs to")
G.add_edge("Faculté d'Informatique", "University1", label="belongs to")
G.add_edge("Faculté SEA", "University2", label="belongs to")

# Relations Universités -> Villes
G.add_edge("University1", "City1", label="locates in")
G.add_edge("University2", "City2", label="locates in")

# Relations Villes -> Pays
G.add_edge("City1", "Cameroun", label="is in")
G.add_edge("City2", "Burkina Faso", label="is in")

# Relations Pays -> Continent
G.add_edge("Cameroun", "Afrique", label="is in")
G.add_edge("Burkina Faso", "Afrique", label="is in")

# Relations Enseignants -> Universités
G.add_edge("Teacher1", "University1", label="teaches at")
G.add_edge("Teacher2", "University2", label="teaches at")

# Relations Enseignants -> Cours
G.add_edge("Teacher1", "Session Course1", label="gives")
G.add_edge("Teacher2", "Session Course2", label="gives")

# Relations Étudiants -> Sessions
G.add_edge("Student1", "Session Course1", label="follows")
G.add_edge("Student2", "Session Course2", label="follows")

# Relations Étudiants -> Facultés
G.add_edge("Student1", "Faculté des Lettres Modernes", label="signed up")
G.add_edge("Student2", "Faculté SEA", label="signed up")

# Relations Enseignants -> Villes
G.add_edge("Teacher1", "City1", label="lives in")
G.add_edge("Teacher2", "City2", label="lives in")

# Relations Enseignants -> Pays
G.add_edge("Teacher1", "Cameroun", label="comes from")
G.add_edge("Teacher2", "Burkina Faso", label="comes from")

# Collaboration entre enseignants
G.add_edge("Teacher1", "Teacher2", label="collaborates with")

# Relations Cours -> Facultés
G.add_edge("Session Course1", "Faculté des Lettres Modernes", label="is given by")
G.add_edge("Session Course2", "Faculté SEA", label="is given by")

# Affichage du graphe
plt.figure(figsize=(20, 15))
pos = nx.spring_layout(G, seed=42)
nx.draw_networkx_nodes(G, pos, node_color='lightblue', node_size=3000)
nx.draw_networkx_labels(G, pos, font_size=10, font_weight='bold')
nx.draw_networkx_edges(G, pos, arrowstyle='-|>', arrowsize=15, edge_color='gray')
edge_labels = nx.get_edge_attributes(G, 'label')
nx.draw_networkx_edge_labels(G, pos, edge_labels=edge_labels, font_size=8)

plt.title("Graphe : Dispensation des cours dans le système éducatif", fontsize=16)
plt.axis('off')
plt.show()
