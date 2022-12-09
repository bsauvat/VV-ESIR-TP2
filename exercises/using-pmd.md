# Using PMD

Pick a Java project from Github (see the [instructions](../sujet.md) for suggestions). Run PMD on its source code using any ruleset. Describe below an issue found by PMD that you think should be solved (true positive) and include below the changes you would add to the source code. Describe below an issue found by PMD that is not worth solving (false positive). Explain why you would not solve this issue.

## Answer

(Warning) AvoidPrintStackTrace (1 violation)
(Warning) (48,5) ThreadsController.pauser()

private void pauser(){
try{
sleep(speed);
}
catch (InterruptedException e){
e.printStackTrace();
}
}


Cette erreur permet de dévoiler des failles de sécurité pouvant être critiques, en effet en affichant la trace d'exécution, il est possible d’effectuer une rétro ingénierie du code. Un fix pourrait être de gérer l’exception dans la fonction appelant “pauser()” ou bien de supprimer le e.printStackTrace().
