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
    * The loop times N from the *rand(50)* then to rotate the array by _pop, push, shift and unshift_ 
    with N times.
    * If the *rand(50)* mod 3 is equal to 0 then to exchange the elements of array. For instance
    ```perl
    @ary[n,n+1] = @ary[n+1,n];
    if($n==$#ary) {
      @ary[$#ary,0] = @ary[0,$#ary];
    }
    ```
    * If the *rand(50)* mod 5 is equal to 0 then to reverse the array. For example
    ```perl
    @ary = reverse @ary;
    ```
*  To revise the architecture. The origin architecture is

  ```perl
  $schedule{$weekday}{$day}{$class} = $man;
  @timecard;
  ```
  by the some unsoloved reasons, we have this new architecture is

  ```perl
  $schedule{$day} = [$man_A, $man_B, $man_C, $man_D, $man_E];
  $weekdays{$day} = $weekday;
  $timecard{$man} = Total_work_hours;
  ```
*  The _grep_ and _map_ is very awsome useful function in Perl to process the arrays even the hashs.
  For instance
    - To create the array of 0,2,4,6,...$#ary.
    ```perl
	for my $i(map {$_*2} 0..(int($#ary/2)+($#ary%2))) {}
    ```
    - To calculate the total work hours.
    ```perl
	map {$timecard{$schedule{$d}[$_]}+=$class_unit[$_], if($schedule{$d}[$_]!~/^\d/)} 
	0..$#{$schedule{$d}};
    ```
    - To fill the string "None" in the array.
    ```perl
      @{$schedule{$d}}=map {$_="None"} @{$schedule{$d}}, if($weekdays{$d}==7);
    ```
    - We could have the if...else statement in the block of _map_
    ```perl
      @{$schedule{$d}}=map {($_=~/[345]/)?($_="X"):($_=$_)} @{$schedule{$d}}, if($weekdays{$d}==6);
    ```
*  Use the _sort_ to arrange the man power by its work hours.
    ```perl
      my @yesterday = &ary_shuffle(@{$schedule{$d-1}}[0,2,3]);
      @{$schedule{$d}}[1..2] = @yesterday[0..1]; 
      @yesterday[0..1] = @{$schedule{$d-1}}[1,4];
      @{$schedule{$d}}[3,0,4] = sort {$timecard{$a}<=>$timecard{$b}} @yesterday;
    ```
