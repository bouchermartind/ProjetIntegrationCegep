# prog pour faire forme
import os
import turtle

#aller a point
def aller_a(x, y):
    """Déplace stylo not tracer."""
    t.penup()
    t.goto(x, y)
    t.pendown()

#afficher les cordo
def afficher_coord(x, y):
    """Marque point et écrit coordonnées."""
    t.penup()
    t.goto(x, y)
    t.dot(6, "red")
    t.write(f"({x},{y})", font=("Arial", 8, "normal"))


#lire fichier ligne par ligne
def parse_line(line):
    command_vector = line.split()

    print (command_vector)

    command_code = command_vector[0]
    if not command_code.isupper():
        raise ValueError("Premier caractere pas lettre Maj")

    #quoi fair si start L
    if command_code == 'L':
        if len(command_vector) != 5:
            raise ValueError("La commande 'L' nécessite 5 paramètres (L, x1, y1, x2, y2).")
        x1, y1, x2, y2 = map(int, command_vector[1:5])
        print(x1, y1, x2, y2)

        # Ligne
        aller_a(x1, y1)
        t.goto(x2, y2)
        # Coordonnées des deux extrémités
        afficher_coord(x1, y1)
        afficher_coord(x2, y2)

    elif command_code == 'C':
        if len(command_vector) != 4:
            raise ValueError("La commande 'C' nécessite 4 paramètres (C, x1, y1, rayon).")
        x1, y1, rayon = map(int, command_vector[1:4])
        print(x1, y1, rayon)

        # turtle.circle() dessine le cercle DESSUS position :
        # descend 'rayon' pour (x1, y1) = centre (y1-rayon)
        aller_a(x1, y1 - rayon)
        t.circle(rayon)
        # Centre du cercle
        afficher_coord(x1, y1)

#lire ficher et voir        
chemin_fichier = 'C:\\FichiersProg\\texte_Test_DaVinci.txt'
with open(chemin_fichier, 'r') as fichier:
     # La boucle lit et traite chaque ligne une par une jusqu'à la fin
    for line in fichier:
        parse_line(line)

#garde ecran turtle ouvert
turtle.done()
