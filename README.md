# ProgramaJava
/*
 * To change this license header, choose License Headers in Project Properties.
 * To change this template file, choose Tools | Templates
 * and open the template in the editor.
 */
package projetodocs2;

import java.util.Scanner;

/**
 *
 * @author Aluno
 */
public class ProjetoDocs2 {

    /**
     * @param args the command line arguments
     */
    public static void main(String[] args) {
        String rg, test;
        char X, X1;
        int tam, tot=0, resto, digitoR, digitoV, num, multi, iniMulti, i, confere,
        digitoK, digitoP, digitoS, cont=0, max, totNum = 0;
        Scanner s = new Scanner(System.in);
        
        System.out.println("Digite os dígitos de um documento seu");
        rg = s.nextLine();
        tam = rg.length();
        int doc [] = new int [tam];
        for (int a=0; a<tam; a++) {
            num = Character.getNumericValue(rg.charAt(a));
            if (num>=0 && num<10) {
                doc[totNum] = num;
                totNum++;
            }
            if (totNum==8 && rg.charAt(a)=='X' || rg.charAt(a)=='x') {
                totNum++;
                doc[8]=10;
            }
            
        }
            switch (totNum) {
                case 9:
                    iniMulti = 2;
                    max = 8;
                    multi = 2;
                    break;
                case 11:
                    iniMulti = 10;
                    multi = 10;
                    max = 9;
                    break;
                case 14:
                    iniMulti = 5;
                    multi = 5;
                    max = 12;
                    break;
                default:
                    iniMulti = 0;
                    multi = 0;
                    max = 0;
                    System.out.println("Documento inválido");               
            }
  
            for (int z=0;z<max;z++) {
                tot += multi*doc[cont];   
                if (iniMulti==10) {
                    multi--;
                } else if (iniMulti==2){
                    multi++;
                } else if (iniMulti==5) {
                    if (multi==2) {
                        multi=10;
                    }
                    multi--;
                }
                cont++;
            }
            
            resto = tot % 11;
            digitoR = 11 - resto;
 
            switch (iniMulti) {
                case 2:
                    switch (digitoR) {
                        case 10:
                            if (doc[8]==10 || doc[8]==10) {
                                System.out.println("RG válido");
                                for (i=0, confere = 1; i<8; i++, confere++) {
                                    if (confere == 3 || confere == 6) {
                                        System.out.print(".");
                                    }
                                    System.out.print(doc[i]);
                                }
                                System.out.println("-X");
                            }
                            else {
                                System.out.println("RG inválido. \nSeu dígito verificador para este RG seria: X");
                            }
                            break;
                        case 11:
                            digitoR = 0;
                            digitoV = Character.getNumericValue(rg.charAt(tam-1));
                            if (digitoV==digitoR) {
                                System.out.println("RG válido");
                                for (i=0, confere=1; i<8; i++, confere++) {
                                    if (confere == 3 || confere == 6) {
                                        System.out.print(".");
                                    }
                                    System.out.print(doc[i]);
                                }
                                System.out.println("-" + digitoR);
                                
                            }
                            else {
                                System.out.println("RG inválido. Seu dígito verificador para este RG seria: " + digitoR);
                            }
                            break;
                        default:
                            digitoV = Character.getNumericValue(rg.charAt(tam-1));
                            if (digitoV==digitoR) {
                                System.out.println("RG válido");
                                for (i=0, confere=1; i<8; i++, confere++) {
                                    if (confere==3 || confere==6){
                                        System.out.print(".");
                                    }
                                    System.out.print(doc[i]);
                                }
                                System.out.println("-" + digitoR);
                            }
                            else {
                                System.out.println("RG inválido. Seu dígito verificador para este RG seria: " + digitoR);
                            }
                        break;
                    }
                break;
                case 10:
                    switch (digitoR) {
                        case 10:
                        case 11:
                            digitoR = 0;
                            digitoK=0;
                            for (int a=11, b=0; a>=2;a--,b++) {
                                if (a>2) {
                                    digitoK+=doc[b]*a;
                                }
                            }
                            digitoK %= 11;
                            if (digitoK <= 1) {
                                digitoK = 0;
                            }
                            else {
                                digitoK = 11 - digitoK;
                            }
                            digitoP = doc[9];
                            digitoS = doc[10];
                            if (digitoP==0 && digitoS == digitoK) {
                                System.out.println("CPF válido");
                                for (i=0, confere=0; i<9; i++, confere++) {
                                    if (confere % 3 == 0 && confere > 0) {
                                        System.out.print(".");
                                    }
                                    System.out.print(doc[i]);
                                }
                                System.out.println("-" + digitoR + digitoK);
                            }
                            else {
                                System.out.println("CPF inválido. Os dígitos "
                                + "certos para este CPF seriam: " + digitoR + digitoK);
                            }
                        break;
                            
                        default:
                            digitoK = 0;
                            for (int a=11, b=0; a>=2;a--,b++) {
                                if (a>2) {
                                    digitoK+=doc[b]*a;
                                } else {
                                    digitoK+=a*digitoR;
                                }
                            }
                            digitoK %= 11;
                            if (digitoK <= 1) {
                                digitoK = 0;
                            }
                            else {
                                digitoK = 11 - digitoK;
                            }
                            digitoP = doc[9];
                            digitoS = doc[10];
                            if (digitoP==digitoR && digitoS == digitoK) {
                                System.out.println("CPF válido");
                                for (i=0, confere=0; i<9; i++, confere++) {
                                    if (confere % 3 == 0 && confere > 0) {
                                        System.out.print(".");
                                    }
                                    System.out.print(doc[i]);
                                }
                                System.out.println("-" + digitoR + digitoK);
                            }
                            else {
                                System.out.println("CPF inválido. Os dígitos "
                                + "certos para este CPF seriam: " + digitoR + digitoK);
                            }
                    }
                break;
                case 5:
                    switch (digitoR) {
                        case 10:
                        case 11:
                            digitoR = 0;
                            digitoK = 0;
                            multi=6;
                            cont = 0;
                            for (int z=0;z<max;z++) {
                                digitoK += multi*doc[cont];
                                
                                if (multi==2) {
                                   multi=10;
                                }
                                multi--;
                                cont++;
                            }
                            digitoK %= 11;
                            if (digitoK <= 1) {
                                digitoK = 0;
                            }
                            else {
                                digitoK = 11 - digitoK;
                            }
                            digitoP = doc[12];
                            digitoS = doc[13];
                            if (digitoP==digitoR && digitoS == digitoK) {
                                System.out.println("CNPJ válido");
                                for (i=0, confere=0; i<12; i++, confere++) {
                                    if (confere==2 || confere==5) {
                                        System.out.print(".");
                                    } else if (confere==8) {
                                        System.out.print("/");
                                    }
                                    System.out.print(doc[i]);
                                }
                                System.out.println("-" + digitoR + digitoK);
                            }
                            else {
                                System.out.println("CNPJ inválido. Os dígitos "
                                + "certos para este CNPJ seriam: " + digitoR + digitoK);
                            }
                        break;
                        default:
                            digitoK = 0;
                            multi=6;
                            cont = 0;
                            for (int z=0;z<=max;z++) {
                                if (z==max) {
                                    digitoK += multi*digitoR;   
                                } else {
                                digitoK += multi*doc[cont];  
                                }
                                
                                if (multi==2) {
                                    multi=10;
                                }
                                multi--;
                                cont++;
                            }
                            
                                digitoK %= 11;
                                
                                if (digitoK <= 1) {
                                    digitoK = 0;
                                }
                                else {
                                    digitoK = 11 - digitoK;
                                }
                                digitoP = doc[12];
                                digitoS = doc[13];
                                if (digitoP==digitoR && digitoS == digitoK) {
                                    System.out.println("CNPJ válido");
                                    for (i=0, confere=0; i<12; i++, confere++) {
                                        if (confere==2 || confere==5) {
                                            System.out.print(".");
                                        } else if (confere==8) {
                                            System.out.print("/");
                                        }
                                        System.out.print(doc[i]);
                                    }
                                    System.out.println("-" + digitoR + digitoK);
                                }
                                else {
                                    System.out.println("CNPJ inválido. Os dígitos "
                                    + "certos para este CNPJ seriam: " + digitoR + digitoK);
                                }
                            }
                               
            }
    }
    
}
