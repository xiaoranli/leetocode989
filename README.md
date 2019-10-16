8、leetcode989. 数组形式的整数加法
==
解法一：
--  
思路：
--
    1、先将整形数组 变成 整数。2、在将和添加到list中。  
代码： 
--
<pre>
**
 * @author lihe
 * @date 2019/10/16 10:07
 * @descriptor  989. 数组形式的整数加法
 */
public class AddToArrayForm_989 {
    public static List<Integer> addToArrayForm(int[] A, int K){
        int num = getNum(A);
        int sum = num + K;
        List<Integer> list = new ArrayList<>();
        while(sum > 0){
            list.add(0,sum%10);
            sum /= 10;
        }
        return list;
    }

    private static int getNum(int[] A) {
        int sum = 0;
        for (int i = 0; i < A.length; i++) {
            sum += A[i] * Math.pow(10,A.length-i-1);
        }
        return sum;
    }
    public static void main(String[] args) {
       // int[] A = {1,2,0,0};
       int[] A = {9,9,9,9,9,9,9,9,9,9};
        //int[] A = {2,1,4,7,4,8,3,6,4,6};
        int K = 1;
        List<Integer> list = addToArrayForm1(A, K);
        for (int i = 0; i < list.size(); i++) {
            System.out.print(list.get(i));
        }
    }
   </pre>
   解法一：
--  
思路：
--
   这道题可以逐位将数字加在一起。例如274和181，可以先计算2+1,7+8,4+1。当相加结果大于等于10，就要进位，7+8=15将进位的1加到前一位的计算中去。  
代码： 
--
<pre>
**
 * @author lihe
 * @date 2019/10/16 10:07
 * @descriptor  989. 数组形式的整数加法
 */
public class AddToArrayForm_989 {
    /**
     * 我们可以对以上的想法做一个小变化，让它实现起来更容易 —— 我们将整个加数加入数组表示的数的最低位。
     * 继续之前的例子 123+912123+912，我们把它表示成 [1, 2, 3+912][1,2,3+912]。
     * 然后，我们计算 3+912 = 9153+912=915。
     * 55 留在当前这一位，将 910/10=91910/10=91 以进位的形式加入下一位。
     * 然后，我们再重复这个过程，计算 [1, 2+91, 5][1,2+91,5]。我们得到 9393，33 留在当前位，
     * 将 90/10=990/10=9 以进位的形式加入下一位。继而又得到 [1+9, 3, 5][1+9,3,5]，重复这个过程之后，
     * 最终得到结果 [1, 0, 3, 5][1,0,3,5]。
     */
    public static List<Integer> addToArrayForm1(int[] A, int K) {
        List<Integer> list = new ArrayList();
        int i = A.length;
        while(--i >= 0 || K > 0){
            if(i >= 0) {
                K = K + A[i];
            }
            list.add(0, K % 10);
            K = K / 10;
        }
        return  list;
    }

    public static void main(String[] args) {
       // int[] A = {1,2,0,0};
       int[] A = {9,9,9,9,9,9,9,9,9,9};
        //int[] A = {2,1,4,7,4,8,3,6,4,6};
        int K = 1;
        List<Integer> list = addToArrayForm1(A, K);
        for (int i = 0; i < list.size(); i++) {
            System.out.print(list.get(i));
        }
    }
   </pre>
