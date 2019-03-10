# Memento JDBC

Ce fichier expose des exemples simple d'utilisation de JDBC

## Connexion a la base de données


## Selection 

`ResultSet résultats = null;
String requete = "SELECT * FROM LesCages";
try {
    Statement stmt = con.createStatement();
    résultats = stmt.executeQuery(requete);
    
    //affichage des enregistrements existants
    System.out.println("** Table LesCages **\nnoCage" + "\t\t" + "fonction" + "\t\t" + "noAllee");
    while (cages.next()) {
        int noCage = cages.getInt(1);
        String fonction = cages.getString(2);
        int noAllee = cages.getInt(3);
        arrayCages.add(""+noCage);
        System.out.println(noCage + "\t\t" + fonction + "\t\t" + noAllee);
    }
} catch (SQLException e) {
    System.err.println("failed");
    System.out.println("Affichage de la pile d'erreur");
    e.printStackTrace(System.err);
}`

## Insertion

`requete = "INSERT INTO client VALUES (4,'client 4','prenom 4')";
try {
    Statement stmt = con.createStatement();
    ResultSet résultats = stmt.executeQuery(requete);
} catch (SQLException e) {
    e.printStackTrace();
}`

## Mise à jour