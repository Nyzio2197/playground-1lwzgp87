// Alan Xiao
// Input through file named input.txt

package ACSL;

import java.io.File;
import java.io.FileNotFoundException;
import java.util.ArrayList;
import java.util.Scanner;

public class Junior_Alan_Contest_2 {
	
	private static final String[] ALPHABET = "abcdefghijklmnopqrstuvwxyz".split("");
	private static final String[] VOWELS = "aeiou".split("");
		
	public static void main(String[] args) {
		try {
			Scanner in = new Scanner(new File("input.txt"));
			final String input = in.nextLine();
			in.close();
			System.out.println(countDifferentLetters(input));
			System.out.println(countVowels(input));
			System.out.println(countUppercaseLetters(input));
			System.out.println(countMostOccuringLetter(input));
			System.out.println(longestWord(input));
			
		} catch (FileNotFoundException ex) {
			
		}
		
	}
	
	public static int intValueOfCharacter(String character) {
		for(int n = 0; n < ALPHABET.length; n++) {
			if(character.equalsIgnoreCase(ALPHABET[n])) {
				return n;
			}
		}
		return -1;
	}
	
	public static int countDifferentLetters(String in) {
		boolean[] lettersUsed = new boolean[26];
		String[] input = in.split("");
		for(int n = 0; n < input.length; n++) {
			if(intValueOfCharacter(input[n]) != -1) {
				if(!lettersUsed[intValueOfCharacter(input[n])]) {
					lettersUsed[intValueOfCharacter(input[n])] = true;
				}
			}
		}
		int differentLetters = 0;
		for(int n = 0; n < lettersUsed.length; n++) {
			if(lettersUsed[n]) {
				differentLetters++;
			}
		}
		return differentLetters;
	}
	
	public static int countVowels(String in) {
		int count = 0;
		String[] input = in.split("");
		for(int a = 0; a < input.length; a++) {
			for(int b = 0; b < VOWELS.length; b++) {
				if(input[a].equalsIgnoreCase(VOWELS[b])) {
					count++;
				}
			}
		}
		return count;
	}
	
	public static int countUppercaseLetters(String in) {
		int count = 0;
		String[] input = in.split("");
		for(int a = 0; a < input.length; a++) {
			for(int b = 0; b < ALPHABET.length; b++) {
				if(input[a].equals(ALPHABET[b].toUpperCase())) {
					count++;
				}
			}
		}
		return count;
	}

	public static int countMostOccuringLetter(String in) {
		int[] lettersUsed = new int[26];
		String[] input = in.split("");
		for(int n = 0; n < input.length; n++) {
			if(intValueOfCharacter(input[n]) != -1) {
				lettersUsed[intValueOfCharacter(input[n])]++;
			}
		}
		int mode = 0;
		for(int n = 0; n < lettersUsed.length; n++) {
			if(lettersUsed[n] > mode) {
				mode = lettersUsed[n];
			}
		}
		return mode;
	}

	public static String[] cleanedInput(String in) {
		return null;
	}
	
	public static String longestWord(String in) {
		String[] input = cleanedInput(in);
		ArrayList<String> longest = new ArrayList<String>();
		longest.add(input[0]);
		for(int n = 1; n < input.length; n++) {
			if(input[n].length() == longest.get(0).length()) {
				longest.add(input[n]);
			} else if(input[n].length() > longest.get(0).length()) {
				longest = new ArrayList<String>();
				longest.add(input[n]);
			}
		}
		longest.sort(String::compareToIgnoreCase);
		return longest.get(0);
	}
}


