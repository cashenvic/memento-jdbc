# Memento JDBC

Voici plein d'exemples si t'as 2 secondes: http://www.mkyong.com/tutorials/jdbc-tutorials/
- Connexion
- L'objet Statement
- L'objet PreparedStatement
- Procedure stockée
- etc

Ou alors t'es vraiment pressé, et là suite est pour toi.

Ce fichier expose des exemples simple d'utilisation de JDBC

## Connexion

```java
final String CONN_URL = "jdbc:oracle:thin:@im2ag-oracle.e.ujf-grenoble.fr:1521:im2ag";
	
final String USER = "A COMPLETER";
final String PASSWD = "A COMPLETER";

Connection conn; 


public static void main(String args[]) {

    try {
        DriverManager.registerDriver(new oracle.jdbc.driver.OracleDriver());
        
        // Etablissement de la connection
        System.out.print("Connecting to the database... "); 
        conn = DriverManager.getConnection(CONN_URL,USER,PASSWD);
        System.out.println("connected");
        
        conn.setAutoCommit(true); //il faut le mettre mais je sais pas a quoi ça sert :)
        
        // code métier
        
        // code métier
  	    
    } catch (SQLException e) {
        System.err.println("failed");
        System.out.println("Affichage de la pile d'erreur");
        e.printStackTrace(System.err);
        System.out.println("Affichage du message d'erreur");
        System.out.println(e.getMessage());
        System.out.println("Affichage du code d'erreur");
        System.out.println(e.getErrorCode());	    

    } finally {
        //tout ce qui a été ouvert doit etre fermé
        conn.close();
        
        //Les ResultSet et les Statement doivent etre remis à null
    }
 }
```

## Selection 

```java
ResultSet resultats = null;
// Requete à executer
String requete = "SELECT * FROM LesCages";
try {
    //Creation de l'objet de la requete
    Statement stmt = conn.createStatement();
    resultats = stmt.executeQuery(requete);
    
    //affichage des enregistrements existants
    System.out.println("** Table LesCages **\nnoCage" + "\t\t" + "fonction" + "\t\t" + "noAllee");
    
    // Parcours des resulats (objet ResulSet) retournés par executeQuery(requete)
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
} finally {
    //les connexions doivent etre fermées
    
    //les ReseultSet et les Statement doivent etre mis à null
    resultats = null;
    stmt = null;
}

```

## Insertion

Exemple d'insertion

```java
requete = "INSERT INTO client VALUES (4,'client 4','prenom 4')";
try {
    Statement stmt = conn.createStatement();
    ResultSet resultats = stmt.executeQuery(requete);
} catch (SQLException e) {
    e.printStackTrace();
}
```

## Mise à jour

```java
String sql = "update employee set name=? where emp_id=?";

try {
    PreparedStatement stmt = conn.prepareStatement(sql);
    stmt.setString(1, "Henry Ellenson");
    stmt.setInt(2, 2);
    stmt.executeUpdate();
    
    System.out.println("Database updated successfully ");
} catch (SQLException e) {
    e.printStackTrace();
} finally {
    //fermeture de la connexion
    conn = null;
    //Remise de la Statement à null
    stmt = null;
}
```

## PreparedStatement

Exemple de **Select** avec une **requete preparee**

```java
try {
    PreparedStatement ps;
    ps = conn.prepareStatement("SELECT * FROM personnes WHERE nom_personne = ?");
    ps.setString(1, "nom3");
    ResultSet resultats = ps.executeQuery();
    
    // Parcours des resulats (objet ResulSet) retournés par executeQuery()
    boolean encore = resultats.next();
    while (encore) {
        System.out.print(resultats.getInt(1) + " : "+resultats.getString(2)+" "+
        resultats.getString(3)+"("+resultats.getDate(4)+")");
        System.out.println();
        encore = resultats.next();
    }
    resultats.close();
} catch (SQLException e) {
    arret(e.getMessage());
}
```

## Exemples de procedure stockée

https://www.journaldev.com/2502/callablestatement-in-java-example `Recommandé`

https://java.developpez.com/faq/jdbc/?page=Les-procedures-stockees-et-fonctions-moins-CallableStatement

https://www.boraji.com/jdbc-calling-mysql-stored-procedure-example

https://www.boraji.com/jdbc-callablestatement-resultset-example

```java
```
