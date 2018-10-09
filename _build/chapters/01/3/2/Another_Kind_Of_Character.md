---
interact_link: content/chapters/01/3/2/Another_Kind_Of_Character.ipynb
title: 'Another Kind of Character'
prev_page:
  url: /chapters/01/3/1/Literary_Characters
  title: 'Literary Characters'
next_page:
  url: /chapters/02/causality-and-experiments
  title: 'Causality and Experiments'
comment: "***PROGRAMMATICALLY GENERATED, DO NOT EDIT. SEE ORIGINAL FILES IN /content***"
---

# Another Kind of Character

In some situations, the relationships between quantities allow us to make predictions. This text will explore how to make accurate predictions based on incomplete information and develop methods for combining multiple sources of uncertain information to make decisions.

As an example of visualizing information derived from multiple sources, let us first use the computer to get some information that would be tedious to acquire by hand. In the context of novels, the word "character" has a second meaning: a printed symbol such as a letter or number or punctuation symbol. Here, we ask the computer to count the number of characters and the number of periods in each chapter of both *Huckleberry Finn* and *Little Women*.



{:.input_area}
```python
# In each chapter, count the number of all characters;
# call this the "length" of the chapter.
# Also count the number of periods.

chars_periods_huck_finn = Table().with_columns([
        'Huck Finn Chapter Length', [len(s) for s in huck_finn_chapters],
        'Number of Periods', np.char.count(huck_finn_chapters, '.')
    ])
chars_periods_little_women = Table().with_columns([
        'Little Women Chapter Length', [len(s) for s in little_women_chapters],
        'Number of Periods', np.char.count(little_women_chapters, '.')
    ])
```


Here are the data for *Huckleberry Finn*. Each row of the table corresponds to one chapter of the novel and displays the number of characters as well as the number of periods in the chapter. Not surprisingly, chapters with fewer characters also tend to have fewer periods, in general – the shorter the chapter, the fewer sentences there tend to be, and vice versa. The relation is not entirely predictable, however, as sentences are of varying lengths and can involve other punctuation such as question marks. 



{:.input_area}
```python
chars_periods_huck_finn
```





<div markdown="0">
<table border="1" class="dataframe">
    <thead>
        <tr>
            <th>Huck Finn Chapter Length</th> <th>Number of Periods</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>7,026                   </td> <td>66               </td>
        </tr>
    </tbody>
        <tr>
            <td>11,982                  </td> <td>117              </td>
        </tr>
    </tbody>
        <tr>
            <td>8,529                   </td> <td>72               </td>
        </tr>
    </tbody>
        <tr>
            <td>6,799                   </td> <td>84               </td>
        </tr>
    </tbody>
        <tr>
            <td>8,166                   </td> <td>91               </td>
        </tr>
    </tbody>
        <tr>
            <td>14,550                  </td> <td>125              </td>
        </tr>
    </tbody>
        <tr>
            <td>13,218                  </td> <td>127              </td>
        </tr>
    </tbody>
        <tr>
            <td>22,208                  </td> <td>249              </td>
        </tr>
    </tbody>
        <tr>
            <td>8,081                   </td> <td>71               </td>
        </tr>
    </tbody>
        <tr>
            <td>7,036                   </td> <td>70               </td>
        </tr>
    </tbody>
</table>
<p>... (33 rows omitted)</p>
</div>



Here are the corresponding data for *Little Women*.



{:.input_area}
```python
chars_periods_little_women
```





<div markdown="0">
<table border="1" class="dataframe">
    <thead>
        <tr>
            <th>Little Women Chapter Length</th> <th>Number of Periods</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>21,759                     </td> <td>189              </td>
        </tr>
    </tbody>
        <tr>
            <td>22,148                     </td> <td>188              </td>
        </tr>
    </tbody>
        <tr>
            <td>20,558                     </td> <td>231              </td>
        </tr>
    </tbody>
        <tr>
            <td>25,526                     </td> <td>195              </td>
        </tr>
    </tbody>
        <tr>
            <td>23,395                     </td> <td>255              </td>
        </tr>
    </tbody>
        <tr>
            <td>14,622                     </td> <td>140              </td>
        </tr>
    </tbody>
        <tr>
            <td>14,431                     </td> <td>131              </td>
        </tr>
    </tbody>
        <tr>
            <td>22,476                     </td> <td>214              </td>
        </tr>
    </tbody>
        <tr>
            <td>33,767                     </td> <td>337              </td>
        </tr>
    </tbody>
        <tr>
            <td>18,508                     </td> <td>185              </td>
        </tr>
    </tbody>
</table>
<p>... (37 rows omitted)</p>
</div>



You can see that the chapters of *Little Women* are in general longer than those of *Huckleberry Finn*. Let us see if these two simple variables – the length and number of periods in each chapter – can tell us anything more about the two books. One way for us to do this is to plot both sets of data on the same axes. 

In the plot below, there is a dot for each chapter in each book. Blue dots correspond to *Huckleberry Finn* and gold dots to *Little Women*. The horizontal axis represents the number of periods and the vertical axis represents the number of characters.



{:.input_area}
```python
plots.figure(figsize=(6, 6))
plots.scatter(chars_periods_huck_finn.column(1), 
              chars_periods_huck_finn.column(0), 
              color='darkblue')
plots.scatter(chars_periods_little_women.column(1), 
              chars_periods_little_women.column(0), 
              color='gold')
plots.xlabel('Number of periods in chapter')
plots.ylabel('Number of characters in chapter');
```



![png](../../../../images/build/chapters/01/3/2/Another_Kind_Of_Character_7_0.png)


The plot shows us that many but not all of the chapters of *Little Women* are longer than those of *Huckleberry Finn*, as we had observed by just looking at the numbers. But it also shows us something more. Notice how the blue points are roughly clustered around a straight line, as are the yellow points. Moreover, it looks as though both colors of points might be clustered around the *same* straight line.

Now look at all the chapters that contain about 100 periods. The plot shows that those chapters contain about 10,000 characters to about 15,000 characters, roughly. That's about 100 to 150 characters per period.

Indeed, it appears from looking at the plot that on average both books tend to have somewhere between 100 and 150 characters between periods, as a very rough estimate. Perhaps these two great 19th century novels were signaling something so very familiar to us now: the 140-character limit of Twitter.
