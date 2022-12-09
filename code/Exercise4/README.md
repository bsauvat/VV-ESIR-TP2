# Code of your exercise

package org.example;

import com.github.javaparser.ast.CompilationUnit;
import com.github.javaparser.ast.body.*;
import com.github.javaparser.ast.visitor.VoidVisitorWithDefaults;

import java.util.ArrayList;


// This class visits a compilation unit and
// prints all public enum, classes or interfaces along with their public methods
public class PublicElementsPrinter extends VoidVisitorWithDefaults<Void> {

    private ArrayList<String> publicMethods = new ArrayList<>();

    @Override
    public void visit(CompilationUnit unit, Void arg) {
        for(TypeDeclaration<?> type : unit.getTypes()) {
            type.accept(this, null);
        }
    }

    public void visitTypeDeclaration(TypeDeclaration<?> declaration, Void arg) {
        if(!declaration.isPublic()) return;
        System.out.println(declaration.getFullyQualifiedName().orElse("[Anonymous]"));
        for(MethodDeclaration method : declaration.getMethods()) {
            if (method.getAccessSpecifier().toString().equals("PUBLIC") && !method.getType().toString().equals("void")) {
                String methodeName = method.getNameAsString();
                if (methodeName.startsWith("get")) {
                    String name = methodeName.split("get")[1];
                    publicMethods.add(name);
                }
            }
            method.accept(this, arg);
        }
        // Printing nested types in the top level
        for(BodyDeclaration<?> member : declaration.getMembers()) {
            if (member instanceof FieldDeclaration) {
                if (((FieldDeclaration) member).isPrivate()) {
                    String name = String.valueOf(((FieldDeclaration) member).getVariable(0).getName());
                    if (!publicMethods.contains(name)) {
                        System.out.println("-" + name);
                    }
                }
            }
            if (member instanceof TypeDeclaration)
                member.accept(this, arg);
        }

    }

    @Override
    public void visit(ClassOrInterfaceDeclaration declaration, Void arg) {
        visitTypeDeclaration(declaration, arg);
    }

    @Override
    public void visit(EnumDeclaration declaration, Void arg) {
        visitTypeDeclaration(declaration, arg);
    }

    @Override
    public void visit(MethodDeclaration declaration, Void arg) {
        if(!declaration.isPublic()) return;
        // System.out.println("  " + declaration.getDeclarationAsString(true, true));
    }

}