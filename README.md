#Angus\_schedule
### Rule
|Class | Hours | Mon | Tue | Wed | Thu | Fri | Sat |
| :---: | :---: | :---: | :---: | :---: | :---: |:---: | :---: |
| 1 | 7.5 | :u55b6: | :u55b6: | :u55b6: | :u55b6: | :u55b6: | :u7981: |
| 2 | 7.5 | :u55b6: | :u55b6: | :u55b6: | :u55b6: | :u55b6: | :u7981: |
| 3 | 7.5 | :u55b6: | :u55b6: | :u55b6: | :u55b6: | :u55b6: | :u7981: |
| 4 | 8 | :u55b6: | :u55b6: | :u55b6: | :u55b6: | :u55b6: | :u7981: |
| 5 | 6.5 | :u55b6: | :u55b6: | :u55b6: | :u55b6: | :u55b6: | :u7981: |
| 6 | 9 | :no\_entry: |:no\_entry: |:no\_entry: |:no\_entry: |:no\_entry: | :u55b6: |
| 7 | 9 | :no\_entry: |:no\_entry: |:no\_entry: |:no\_entry: |:no\_entry: | :u55b6: |
| 8 | 9 | :no\_entry: |:no\_entry: |:no\_entry: |:no\_entry: |:no\_entry: | :u55b6: |

The table show the detail of schedule

### Special rule
* Class 2 or 5 (Today) forbid work on Class 2 and 3 (Tomorrow)
* The class 2 or 5 on Tue forbid work on class 1 and 3 on Wed
* Basiclly the work hours of month is 160
* 中文測試

### Reviews

* To search the array **day\_off** from another array **staff**
 - The array day\_off only two elements.
```perl
  @ary = grep {$_ =~ /[^$day_off[0][1]]/} grep {$_ =~ /[^$day_off[0][0]]/} @staff;
```
* Negate smart match
 - More clever search with smart match
```perl  
  @ary = grep  {!($_ ~~ @{$day_off[0]})} @staff;
```

* The *rand()* function isn't my expectation for the array which have few elements.
  - New function *ary_shuffle* 
    * If *rand(50)* mod 2 is equal to 0 then to reverse the array.
    ```perl
    @ary = reverse @ary;
    ```
    * If *rand(50)* mod 3 is equal to 0 then to exchange the elements of array.
    ```perl
    @ary[1,2] = @ary[2,1];
    ```
    * If *rand(50)* mod 5 is equal to 0 then to rotate the array by *pop, push, shift and unshift*

