m# Extending PMD

Use XPath to define a new rule for PMD to prevent complex code. The rule should detect the use of three or more nested `if` statements in Java programs so it can detect patterns like the following:

```Java
if (...) {
    ...
    if (...) {
        ...
        if (...) {
            ....
        }
    }

}
```
Notice that the nested `if`s may not be direct children of the outer `if`s. They may be written, for example, inside a `for` loop or any other statement.
Write below the XML definition of your rule.

You can find more information on extending PMD in the following link: https://pmd.github.io/latest/pmd_userdocs_extending_writing_rules_intro.html, as well as help for using `pmd-designer` [here](https://github.com/selabs-ur1/VV-ESIR-TP2/blob/master/exercises/designer-help.md).

Use your rule with different projects and describe you findings below. See the [instructions](../sujet.md) for suggestions on the projects to use.

## Answer

En utilisant notre règle nous obtenons le PMD report suivant :

1 C:\Users basti DocumentsiCours_4eme_annee|VVicommons-math-master.commons-math.
Line 401

corelsre main java lorg apache \commons \math4 \core jdkmath AccurateMath.java

2 C:Users basti Documents| Cours_4eme_anneelVVicommons-math-master\commons-math-core'sre'main/javalorglapache commons math4 core jdkmath Accurate Math,java
Line 471

3 C:\Users basti Documents|Cours_4eme_annee|VVcommons-math-master\commons-math-corelsre main java lorg lapache commons math4 core jdkmath AccurateMath.java
Line 720

4 C: Users basti Documents Cours 4eme_anneelVVIcommons-math-master commons-math-corelsre lmain javalorg lapache (commons math4 core ljdkmath AccurateMath. java
Line 722

5 C: Users basti Documents\ Cours_4eme_anneelVVIcommons-math-master commons-math.
corelsre main java lorg lapache commons math4 core jdkmath AccurateMath.java
Line 750

6 C: Users basti Documents Cours_ 4eme_anneelYVicommons-math-master commons-math-
core sre main java lorg apache commons math4 \core jdkmath AccurateMath.iava
Line 752

7 C:Users basti Documents Cours 4eme anneeIVVicommons-math-mastericommons-math-core\sre main javalorg lapache commons math4 core jdkmath AccurateMath.java
Line 859

8 C:\Users basti Documents\Cours_4eme_anneelVVcommons-math-master'commons-math core sre main java lorg lapache commons math4 core jdkmath AccurateMath.java
Line 869

9 C:\Users basti Documents Cours 4eme annee\VV\commons-math-mastercommons-math-core lsre main java lorg lapache commons math4 core jdkmath AccurateMath:java
Line 879

10 C: Users basti Documents Cours 4eme annee|VVcommons-math-master\commons-math-core lsre main java lorg apache commons math4 core jdkmath AccurateMath.java
Line 889

Nous obtenons des informations sur le report et un certain nombre de problèmes à résoudre avec des lignes associées à chacune de nos erreurs