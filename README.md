# Expression-Evaluation
This program evaluates the value of the infix expression and it handles the exception cases in which it displays the respective error.

package expression_evaluation;
import java.util.Scanner;
import java.util.Stack;
import java.util.StringTokenizer;

// Written by Ikshita Gupta
//This program evaluates the value of the infix expression
//Also it handles the exception cases in which it displays the respective error

public class ExpressionEvaluation {
   public static void main(String[] args) {
      String input = ""; 
      int result;
      Scanner s = new Scanner(System.in);
      System.out.println("Enter the expression you want to evaluate:");
      input = s.nextLine();
      result = evaluateExpression(input);
      System.out.println("The calculate expression is "+result );
    }
    
   public static int evaluateExpression(String expression){
      int finalResult;
      Stack<Integer> value;
      value = new Stack<Integer>();
      Stack<Character> op;
      op = new Stack<Character>();
      String token ;
      token = "";
      int flag = 1;
      expression = expression.replaceAll("\\s", "#");
      StringTokenizer tokenizer1 ;
      tokenizer1 = new StringTokenizer(expression, "#+-*", true);
        while(tokenizer1.hasMoreTokens()){
           token = tokenizer1.nextToken();
        if(token.compareTo("0")>=0 && flag==1)
           flag=2;
        else if((token.equals("+")|| token.equals("-")||token.equals("*")) && flag==2)
           flag=1;
         else if((token.equals("#") && (flag==2 || flag == 1)))
           continue;
        else{
           if(flag == 1)
               System.out.println("Invalid Expression: More operator error");
           if(flag == 2)
               System.out.println("Invalid Expression: More operand error");
           System.exit(0);
        }
       }
      StringTokenizer tokenizer ;
      
      tokenizer = new StringTokenizer(expression, "#+-*", true);
      
      while(tokenizer.hasMoreTokens()){
         token = tokenizer.nextToken();
      if(token.equals("#"))
         continue ;
      if(token.compareTo("0")>=0){
         value.push(Integer.parseInt(token));
      }
      if(token.equals("+")|| token.equals("-")||token.equals("*")){
         while(!op.empty() &&  checkPrecedence(token.charAt(0) , op.peek())){
            int   val1 , val2 , r;
            char topOp;
            val1 = value.pop();
            val2 = value.pop();
            topOp = op.pop();
            r = calculate(topOp, val1, val2);
            value.push(r);
        }
         op.push(token.charAt(0));
       }
      }
      while(!op.empty() ){
         value.push(calculate(op.pop(), value.pop(),value.pop()));
     }
      
      finalResult = value.pop();
      return finalResult; 
   }
    
public static boolean checkPrecedence(char op1, char op2){
   if(op1 == '*' &&  (op2 == '+'|| op2 == '-'))
      return false;
   else
      return true;
  }
 public static int calculate(char c , int a , int b){
    switch (c){
     case '+': 
                  return a+b;
          case '-': 
                  return a-b;
              case '*': 
                  return a*b;
          }
          return 0 ;
      }
}
