---
layout: single
title: "cmpnyinfo: the planning"
categories: other 
---

## Introduction

I am trying to make a website, where the users can search up a name of a company in the _KOSPI(Korean Composite Stock Price Index)_, and get the basic financial information of the company over the past decade or so.

Here's what I mean by 'financial information.'

1. Different types of incomes (Net Income, Operating Income, etc)

2. Ratios (ROA, ROE, PER, D/E, etc)

3. Others (market cap, stock prices, etc)

It is basically providing people a easy-to-access, easy-to-read financial statements of their company in interest, along with some essential analytical datas, ***ALL REPRESENTED IN GRAPHS***, so that you can effectively read the trend.

There are already websites like investing, but I want a more _light-weight, casual_ and mobile friendly website, _without all the pop up adds and advertisement videos playing in the corner._ 

**Key Values/Goals**

1. Light-weight

2. Casual

3. Simple

## General Structure (for now)

Whenever I have to build something in a level any bigger than a single, file, I draw out the general structure. Like this.
![draw.io](/assets/img/cmpnyinfo_general_struct.png)

Sorry for the unreadable texts. Here's the url to the [diagram](https://viewer.diagrams.net/?tags=%7B%7D&highlight=0000ff&edit=_blank&layers=1&nav=1&title=cmpnyinfo.drawio#R5Vxbc9o4FP41zHQfYCzJNuaRELabTpPQkE67%2B5IxtgJujEVtE0J%2F%2FUq%2BWxLFIRYhTWca7GMhW9%2B5Hx%2FRQaPl08fQXi0uiYv9DtTcpw4670AIAQL0g1G2KaWvwZQwDz03JYGSMPV%2B4YyoZdS15%2BKoNjAmxI%2B9VZ3okCDATlyj2WFINvVh98Sv33Vlz7FAmDq2L1K%2FeW68SKkW7Jf0f7A3X%2BR3BuYgvbK088HZSqKF7ZJNhYTGHTQKCYnTo%2BXTCPsMvByX9Ht%2F77haPFiIg7jJF%2BzZr%2FuL%2FzY%2FvHh7Nxr9d%2B4Qfdo101kebX%2BdLTh72HibI0Cfe8UOna3vBS4OUQedbRZejKcr22EXNpTzlLaIlz49A%2FRwRtZ0pPt5VhBs52EeMur1OqbT4IwepfwGBj0W15Mt8RGHMX6qkLL1fcRkieNwS4fkV3OpyYQNWNn5pmSdbma0RYVt0DQykcnEZV7MXSJKDzJQ5QBfdc%2BG01%2Fb7vnV5e2teXlxBlbdLvijAEb9OsDQMASAgQxgYGiKAEb7AQ5TtDJI9kAbktiOPRLQ0%2B5AowTb9%2BbszMf3cUtiyqFo5DajiiKUoGiqAlEXQPx60YGmvWTgBLNoVSy8AitdbVzHLopD8oBHxCchpQSEieHZvef7HCmH1KEYYko%2FY9h51OgOswtLz3XZbaTMKtmptcMPqHH80EV%2ByIRaB4rYYbw9mUaDU5Np0bUNJ0yofbbiWUiP5vEfLdY6PDGx7u8Xaxy4Qxa1MRR9O4o8h5fkKkgUm3D7vXryLzvpQSM%2FP3%2BqXj3f5mdPXvw9m5IdV79GT8tvsZPtPpZEZB06eL95je1wjuP9IovdWkwqMrjCQEPCwJwWYp%2Bq%2FWM9kpVxNbvDhHh0ZaVZtHaodD5Fuu7sW9XIk5sIcWGZAbiJUmCEiRIhK5Z9uNxZErlLzcAClGYgpdyT5MlLkTR%2Frkl%2BoZuGU0M6AMDVU%2Fq17Ho%2B0T%2B3t5NkSDoffeB0yvptKFm8t%2Bs95qQRWa7sgPE6sJeYjo4ow8vvVka2aL8iapC8YE4JRnl2S1bMbUBth9ki1CDd%2B4nGLqh5w4ESD21yEqRJvAsyRFWwVHmXgSBTl7YX5Akl1D5sNpues1wFWy%2B4Jz2HLP8SOBVtvKVvB7scQoWDLUDY7XPuAOlicmTIPHQxsP3kSBNQjLAdOlTUtZkdvizoETH7LSObR%2B8w8RRVKCVIQgOJSEJlQDZIM18WMapC0%2BAydr0Et4qm3hfRBJrZU5a2QwHQz17EPAO5p39S8%2BzhqEXry8XkrcaOyiRfUmCRhZTKzDAQM9c3IvhQH%2FQsqwamaRaUql%2FL11iT%2FQor2gdVzD8vaPhMWAib%2FFkwD7fBs4hCqUAD1ORPLbGt3%2Bd1AOTGYo8SIGVK0KCK%2B2aUoCjGvK4KiLnqt1zeNRbRpVkAXno2nYveQ5t78WI9S47fl0IYiFcIqBs9iU5YEiaq0wkx6Stzqp0xOr2Vk466Y3nXqYXspiWmPdKQXVfncMXE5%2Bghe8HbNx2z50b61a32AXAOQE%2FXa3AaPR01s9tQRz2AVIEqvg46Cz1cxuxsFVkwM5IVgyuVGEkRiJnybmaVmf0v6ud8FSifKKK3lM5UvrDrOqnRHyaexYuZR5FNWT5%2Furjy%2BVl5KLmPUGOq1YlOd2lbHFH%2F5trbZD7iPKQudUGFhi6CFZf%2BoMWyVeEklUzqRUaiMxg%2FROmi6Wp3XH3W%2Bt9yDHKAQUJ1RylJSwuDXy8hKLPup5KYHgCmJQTlrCwDGtt3ZZiKeemZHXnO3QULyFlzT8huG9j%2BNvKowmi39sx%2F4wnq89kHNS6hYtG4yLujRuNQzFBv8CMOMjemXV%2Bkn1fZ5831MD8Y04PxZEr%2FTsY3KZHEC8w4PWctZ9HePoVD1eyoFguhpiarDfUKLZ96i%2B6PrxOHjO9%2BeQ8%2FrJHkNVnywvx9aY%2FQ4aRbPcMUWKOqviNljKg838bvzsXzjAFA6pKOyhgxF36XGiMUgJAlvsI5akUUirbMiVgqELOIgIUGH3xCcfyr8qa%2BzAJBjw6YpnmINgk9B0fiIMgGpeEHqx7dlWFH6%2BxX8Ubo%2BQ1eXDcIlPBY3voJlHFZ1L%2Fpl8%2BUcC5ax2M12aroFuWqq4asQH7cnlvxvb0AuLSTK4rtMH5Og5e0T0tVm1bmTfa2aeVydyp9WlwoaaAD%2B7T4hi%2Fd4iZS3KeFGlREW2kQ7Py%2BO3CnBO2VDP2kBKPLNzbr%2BoGS0QVcnwYaNBMNyqukqpcPW7EB0W8eWZc%2F8c4H48Yb9fH0IH2CduW0QW3nmXJ6gJ07uPn1cAOZB4dvTQ8AZ9j6h1rILp%2B2mw1N5Ev1YACfqQdmbTOYIj1osE%2FhMD3QanrQb6gIoK4IfXWKYL5JPUD862Tj0IZuLhc3tSMHCmJ3xg2O12EgZl%2FNX9gnsWm2ARWidmJ3w9wRUVWrfJqE41DZiwkkJk1Jvvtpen3VSWroSzsW013Z20et2Xs77eA3XuzqMr3rkoQqKvlHa7YsRHa%2F7BSNUM1EBSjr9cg3AlW3Ba5cO6ZrhxoJHNZDY9P%2FiQAcrHctqBni1AxKWogLmFpXM2lpsEFD9gllyL9l%2F15vaJyUl7MGPa5gwm%2FuburmuC2NRSGmfS8nFSExG75I2wqoj3JfV%2BGAziucpCZ1XIV7Xk6WuYGjJGSvH4bmPv9ENFTn0jGT3w%2FYVEGNfRO1p6HSX88Qjfz5p%2BHVx2tKG04mCsKVE9lZzNeVCtyP8L5HygjRVL4PRvBbvF%2BdEWL7ZcGIyc31p%2FHoVmDGCzuEXy68fUmgLfNdbfxSgRQ00XWNR4xwEdBoMAmzX9XXc2GQPhDxQrImdHWAyX5I4Jnbt80d27enMQmT3QE7tm%2F%2FqZaE36Mv%2B%2BkkVZZkHn9Z%2FPz%2B5fPXMB4%2F3Vrgk3F3JfGt1Q3WxtklmXkUHoNeUbLZWoBOAvBONLsmkBgVKX7KABR9YtsbNfZAtJutO3GzegNzUP1XtzwNW%2BTa2LIhfXjlv8ujCldUw7Hf7%2BX7qWu7XyR7rGmE0dP6iuAU%2B9qSnRnuOvkViuo%2B0xPfZto%2BwyDqDfp1gwwoJ4DINVnnxwE2hZ6WP0WY5kflDzqi8f8%3D)

**Tech Stack**:

- Git, Github

- Docker

- Python libraries (pandas, plotly, many more)

- DJANGO

- AWS EC2

- SQLite

## Challenges

- ***AWS*** 
  
  - This will be my _first project to use AWS_. I have previouse experience with PaaS (render), but not IaaS. 

- ***Graphs***
  
  - Drawing graphs using the plotly library, and displaying onto the webpage
  
  - handling the graph between the API app and the Web app,
  
  - And all the other minor details. I can already see myself fixing a stupid bug for docker for hours 😭

# Contact Me:

Roger Kim [[GitHub](https://github.com/kmsrogerkim)] [[LinkedIn](https://www.linkedin.com/in/kmsrogerkim/)] 


