---
layout: post
title: "二维数组中的查找《剑指Offer》"
date: 2018/8/24 20:08:24 
image: 'https://i.imgur.com/rVzOJDH.png'
description: 业精于勤，荒于嬉；<br />行成于思，毁于随。
category: 'Java'
tags:
- 二维数组
- 查找算法
introduction: 业精于勤，荒于嬉；<br />行成于思，毁于随。
---
&emsp;&emsp;[牛客网原题地址](https://www.nowcoder.com/practice/abc3fe2ce8e146608e868a70efebf62e?tpId=13&tqId=11154&tPage=1&rp=1&ru=/ta/coding-interviews&qru=/ta/coding-interviews/question-ranking)
<br />
&emsp;&emsp;这道题要求在一个行列都递增的二维数组中找一个数，如下图：
![递增二维数组](https://i.imgur.com/hqBCZqp.png)
&emsp;&emsp;实现代码及思路如下：
![比较思路](https://i.imgur.com/hDlpBC7.png)
{% highlight java %}
package com.example.offer;

/**
 * 在一个二维数组中（每个一维数组的长度相同），
 * 每一行都按照从左到右递增的顺序排序，每一列都按照从上到下递增的顺序排序。
 * 请完成一个函数，输入这样的一个二维数组和一个整数，判断数组中是否含有该整数。
 * @author acer
 *
 */
public class Offer1 {
	
	public static void main(String[] args) {
	/*	
		//先巩固一下基础知识
		
		//**静态**
		//一维数组初始化及打印
		int[] array1 = {1,2,3,4,5,6};
		System.out.println("array1[0]:"+array1[0]);
		//二维数组初始化及打印
		int[][] array2 = {{1,2,3},{4,5,6}};
		System.out.println("array2[0][0]:"+array2[0][0]);
		
		
		//**动态**
		//动态初始化 一维数组
		int[] array3 = new int[6];
		for(int i=0;i<6;i++){
			array3[i]=i+1;
		}
		//foreach 遍历一维数组
		for(int iter:array3){
			System.out.println("iter:"+iter);
		}
	*/	
		
		//动态初始化 二维数组(3行4列)
		int m=3, n=4;
		int[][] twoDArray = new int[m][];  //首先确定行数
        for(int i=0; i<twoDArray.length; ++i){
        	twoDArray[i]=new int[n];     //列的长度每次都变化。每次都要重新申请空间(长度)
            for(int j=0; j<twoDArray[i].length; ++j)
            		twoDArray[i][j]= (j+1)+twoDArray[i].length*i;
        }
    /*   
        //foreach遍历二维数组
        int i=1;
        for(int[] row:twoDArray){
        	System.out.println("row"+i);
        	int j=1;
        	for(int col:row){
        		System.out.println("col "+j+": "+col);
        		j++;
        	}
        	i++;
        }
    */  
        //测试代码
        long t1 = System.nanoTime();
        System.out.println(Find(9,twoDArray));
        long t2 = System.nanoTime();
        System.out.println("程序运行时间为："+(t2-t1)+" ns,注意是纳秒");
				
	}
	
	public static boolean Find(int target, int [][] array) {
		boolean flag = false;  //定义一个布尔值，默认为false，在查找过程中，如果找到了目标数，就把flag只改为 true返回，找不到就返回false
          int rows=array.length;  //获取二维数组的行数
          int columns=array[0].length;  //获取二维数组的列数，这里为了简便，很无耻地认为这就是一个二维矩阵，每一行的列数都相同，直接获取第一行的列数就是所有行的列数(因为博主知道了测试用例哈哈哈)
          if (array != null && rows > 0 && columns > 0) {    
          //因为每一行都从左到右递增，每一列都从上到下递增，
          //即做上角的数最大，右下角的数最小。
          //这里从右上角开始查找，如果要查找的数比右上角的数大，则下移，相当于删除一行；
          //如果要查找的数比右上角的数小，则左移，相当于删除一列；
          //如果不大不小，那就是相等，把flag设为true，break，返回flag，结束查找；
          //如果行列都比较完了，还没有找到，那么flag就是flase。   
            int row = 0;                
            int column = columns - 1;    
            while (row < rows && column >= 0) {    
                int tempValue = array[row][column];    
                if (target > tempValue) {    
                    ++row;    
                } else if (target < tempValue) {    
                    --column;    
                } else {    
                    flag = true;    
                    break;   
                }    
            }    
        }
        return flag;    

    }
	
}
{% endhighlight %}
<br />
<br />
<br />
这里列出一些曾经帮助过我的文章，表示感谢（排名不分先后）：
1. [牛客网原题](https://www.nowcoder.com/practice/abc3fe2ce8e146608e868a70efebf62e?tpId=13&tqId=11154&tPage=1&rp=1&ru=/ta/coding-interviews&qru=/ta/coding-interviews/question-ranking)
2. [岁月淡忘了谁的博客园](https://www.cnblogs.com/henuyuxiang/p/6215663.html)
3. [遥同学的CSDN博客](https://blog.csdn.net/qq_15062527/article/details/48845957)
4. 还有一些没有记录的CSDN博客和简书、知乎等人的文章。
<br />
<br />
<br />
----------
----------
<br />
**万事需坚持，需技巧，虚心请教；<br />走过需担当，需分享，助人助己。**
<br />
----------
----------
<br />
<br />
<br />