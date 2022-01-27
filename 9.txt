package pl.gdynia.amw.opr;
import java.util.ArrayList;


public class Task9 {

    public static int getDigitAt(int position, String string) {
        return Character.getNumericValue(string.charAt(string.length() - position - 1 ));
    }

    public static String multiplyByDigit(String number, int digit) {
        int memory = 0;
        String wynik = "";
        for (int i = 0; i < number.length(); i++) {
            int value = getDigitAt(i, number) * digit + memory;
            memory = value / 10;
            String newNumber = String.valueOf(value % 10);
            wynik = newNumber + wynik;
        }
        wynik = memory + wynik;
        return wynik;
    }

    public static ArrayList<String> multiplyIntoSummableNumbers(String firstNumber, String secondNumber) {
        ArrayList<String> wynik = new ArrayList<>();

        for (int i = 0; i < secondNumber.length(); i++) {
            int multiplier = getDigitAt(i, secondNumber);
            String liczba = multiplyByDigit(firstNumber, multiplier);
            for (int j = 0; j < i; j++) {
                liczba = liczba + "0";
            }
            wynik.add(liczba);
        }
        return wynik;
    }

    public static ArrayList<String> wyrownaj(String firstNumber, String secondNumber) {
        if (firstNumber.length() > secondNumber.length()) {
            int diff = firstNumber.length() - secondNumber.length();
            for (int i = 0; i < diff; i++){
                secondNumber = "0" + secondNumber;
            }
        }

        if (secondNumber.length() > firstNumber.length()) {
            int diff = secondNumber.length() - firstNumber.length();
            for (int i = 0; i < diff; i++){
                firstNumber = "0" + firstNumber;
            }
        }

        ArrayList<String> result = new ArrayList<>();
        result.add(firstNumber);
        result.add(secondNumber);
        return result;
    }

    public static String dodawanie(String firstNumber, String secondNumber){
        ArrayList<String> numbers = Task9.wyrownaj(firstNumber, secondNumber);
        firstNumber = numbers.get(0);
        secondNumber = numbers.get(1);

        int memory = 0;
        String wynik = "";
        for (int i = 0; i < firstNumber.length(); i++) {
            int value = Task9.getDigitAt(i, firstNumber) + Task9.getDigitAt(i, secondNumber) + memory;
            memory = value / 10;
            String newNumber = String.valueOf(value % 10);
            wynik = newNumber + wynik;
        }
        wynik = memory + wynik;
        return wynik;
    }

    public static String dodajWszystkie(ArrayList<String> liczby) {
        String suma = liczby.get(0);
        for (int i = 1; i < liczby.size(); i++){
            suma = dodawanie(suma, liczby.get(i));
        }
        return suma;
    }

}