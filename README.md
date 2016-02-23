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
```
  @ary = grep {$_ =~ /[^$day_off[0][1]]/} grep {$_ =~ /[^$day_off[0][0]]/} @staff;
```
* Negate smart match
 - More clever search with smart match
```
  @ary = grep  {!($_ ~~ @{$day_off[0]})} @staff;
```

* The *rand()* function isn't my expectation for the array which have few elements.
  - New function *ary_shuffle* 
    * The array reverse
    ```
    @ary = reverse @ary;
    ```
    * The element exchange 
    ```
    @ary[1,2] = @ary[2,1];
    ```

