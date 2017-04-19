---
layout: post
title: Merge Sort
author: aay
category: Blog
tags: [Algorithms, Sort, C]
---
Merge sort is a sorting algorithm that is better than the three basic sorting algorithms, selection sort, insertion sort and bubble sort. Merge sort is better in terms of 
its time complexity, which is O(n log(n)). Selection sort, insertion sort and bubble sort each have a complexity of 0(n^2^), which is much slower than O(n log(n)).  

![Big O Complexity](/assets/big-o-complexity.png)  

Now let's get to the algorithm of merge sort.  
Before that, you should look its pseudo code, so that you can get a rough idea of how it works.  

{% highlight python %}
on input of n elements  

	if n < 2
		return
	else
		sort left half of elements  
		sort right half of elements
		merge sorted halves

{% endhighlight %}

Looks really simple, doesn't it? The basic concept of merge sort is clearly very easy to understand.  

First of all, you check the trivial cases of less than 2 elements. If there is only 1 element, then it is already sorted. 
If there are 0 elements, then again, even though meaninglessly, it is sorted, as there is nothing to sort.  

Now, the real stuff- when there are 2 or more elements. Firstly, we obviously assume that they are all stored in an array. Now, How do you 
sort the left and right half of elements? You might have guessed it, merge sort! Again, you sort the left and right halves of the *left* 
half of the original array. And you go on... So there is the concept of recursion in merge sort where at every step, you invoke the same algorithm 
and sort halves.  

Now you may have a basic idea of merge sort. If not, don't worry. Next, we will take an example to help visualise how this works. 
And rest assured, I am going to go really, really, really slow with this.  

Let us take the following array of 4 elements to sort:  

| 8 | 4 | 6 | 2 |  

This array clearly does not contain less than 2 elements, so now we have to sort the left and right halves of the array and then merge them. 
(The third step, **merging**, is very important and must not be forgotten.) Let's get to it straightaway.  
We have to first sort the left half of the array.  

| **8** | **4** | 6 | 2 |  

Now to sort the left half of the array, we use the merge sort algorithm again and sort its left half.  

| **8** | 4 | 6 | 2 |  

We have now reached a stage where there is only 1 element to sort, which is obviously already sorted. The next step? 
Sort the *right* half of the *left* half of the *original array*. Which is  

| 8 | **4** | 6 | 2 |  

Again, we have only 1 element which is already sorted. Now, the third and most important step, merging both the halves. Here it is pretty easy. 
All we have to do is compare both the elements and just place them accordingly in a new array. As 4 is lesser than 8, it will be place first.  

| **8** | **4** | 6 | 2 |  
| **4** | **8** |   |   |  

Phew, now we have successfully sorted the left half of the original array. Time for the right half. 

| 8 | 4 | **6** | **2** |  
| 4 | 8 |   |   |  

We essentially follow the same steps as the left half and get that done. Boom!

| 8 | 4 | 6 | 2 |  
| 4 | 8 | **2** | **6** |  

We have come very close to the end of our sort. The left and the right halves of the array have been sorted individually. 
All we have to do now is merge them. Earlier, there was only 1 element in the right and left half of the arrays each, so merging was very easy. 
Things get slightly tricky now. Focus. First of all, declare a new empty array.  

Point your left index finger to the first element of the left half of the array, which is 4. Point your right finger to the first element of the right 
half of the array, which is 2. Now compare these numbers. 2 is less than 4 so 2 goes first in the new array. Now point your right index finger
to the next element after 2, which is 6. Do nothing to your left finger.  

| 8 | 4 | 6 | 2 |  
| 4 | 8 | 2 | 6 |  
| 2 |   |   |   |  

Compare again. 4 is lesser than 6. It goes next in the new array. And move your left finger to 8.  

| 8 | 4 | 6 | 2 |  
| 4 | 8 | 2 | 6 |  
| 2 | 4 |   |   |  

Compare. 6 is lesser than 8. It goes next. Now your right finger has nothing to point to. That is good news.  

| 8 | 4 | 6 | 2 |  
| 4 | 8 | 2 | 6 |  
| 2 | 4 | 6 |   |  

Now just sequentially add all the remaining elements from the left half. We have only 8 left, so we do that.  

| 8 | 4 | 6 | 2 |  
| 4 | 8 | 2 | 6 |  
| 2 | 4 | 6 | 8 |  

Lo and behold! We have just sorted an array with 4 elements using merge sort. What if we had to sort an array with 8 elements?
All we would have to do is sort the left and right halves of the array as shown and then merge them. The same goes for an array of 
any size. This was just a small cog in a larger wheel.  

You may now be wondering that declaring a new array for every step will take up a lot of memory, but we don't need to declare so many arrays practically.
We can do our sorting using only two arrays. After each step, the previous array becomes useless and so it can be overwritten for the next step.  
Now that the algorithm has been understood, let us look at some actual C code.

{% highlight C %}
#include <stdio.h>
#define max 10

int a[11] = { 10, 14, 19, 26, 27, 31, 33, 35, 42, 44, 0 };
int b[10];

void merging(int low, int mid, int high) {
   int l1, l2, i;

   for(l1 = low, l2 = mid + 1, i = low; l1 <= mid && l2 <= high; i++) {
      if(a[l1] <= a[l2])
         b[i] = a[l1++];
      else
         b[i] = a[l2++];
   }
   
   while(l1 <= mid)
      b[i++] = a[l1++];

   while(l2 <= high)
      b[i++] = a[l2++];

   for(i = low; i <= high; i++)
      a[i] = b[i];
}

void sort(int low, int high) {
   int mid;
   
   if(low < high) {
      mid = (low + high) / 2;
      sort(low, mid);
      sort(mid+1, high);
      merging(low, mid, high);
   } else { 
      return;
   }
}

int main() { 
   int i;

   printf("List before sorting\n");
   
   for(i = 0; i <= max; i++)
      printf("%d ", a[i]);

   sort(0, max);

   printf("\nList after sorting\n");
   
   for(i = 0; i <= max; i++)
      printf("%d ", a[i]);
}
{% endhighlight %}



If we compile and run the above program, it will produce the following result-  

{% highlight ruby %}
List before sorting
10 14 19 26 27 31 33 35 42 44 0
List after sorting
0 10 14 19 26 27 31 33 35 42 44
{% endhighlight %}


















