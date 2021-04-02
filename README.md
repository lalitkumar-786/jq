# JQ
Playing with JSON using JQ

## Prerequisites
JQ should be installed
```
# For MAC
$ brew install jq

# For RHEL/CENT OS
$ yum install jq
```

###1. To list all/beatify the JSON file
  
  ```
  $ cat quiz.json | jq '.'
  ```
  
<details>
  <summary>Output:-</summary>
  
  ```
  {
    "quiz": {
        "sport": {
            "q1": {
                "question": "Which one is correct team name in NBA?",
                "options": [
                    "New York Bulls",
                    "Los Angeles Kings",
                    "Golden State Warriros",
                    "Huston Rocket"
                ],
                "answer": "Huston Rocket"
            }
        },
        "maths": {
            "q1": {
                "question": "5 + 7 = ?",
                "options": [
                    "10",
                    "11",
                    "12",
                    "13"
                ],
                "answer": "12"
            },
            "q2": {
                "question": "12 - 8 = ?",
                "options": [
                    "1",
                    "2",
                    "3",
                    "4"
                ],
                "answer": "4"
            }
        }
    }
}
```
</details>


###2. To list a particular attribute

  ```
  $ cat quiz.json | jq '.quiz.sport'
  
  {
  "q1": {
    "question": "Which one is correct team name in NBA?",
    "options": [
      "New York Bulls",
      "Los Angeles Kings",
      "Golden State Warriros",
      "Huston Rocket"
    ],
    "answer": "Huston Rocket"
  }
}
```
  > Similarly, to get more nested arrtibutes, keep appending the key by '.'
  > e.g:- To get the options field, 
  >
  ```
  $ cat quiz.json | jq '.quiz.sport.q1.options'
  [
  "New York Bulls",
  "Los Angeles Kings",
  "Golden State Warriros",
  "Huston Rocket"
]
  ```


###3. To get all keys
```
$ cat quiz.json | jq '. | keys'

[
  "quiz"
]
```


###4. To get nested keys
```
$ cat quiz.json | jq '.quiz.sport.q1 | keys'

[
  "answer",
  "options",
  "question"
]
```


###5. To check if a key exist

```
## "options" exist as the output is not NULL
$ cat quiz.json | jq '.quiz.sport.q1 | keys[] | select(.=="options")'

"options"

## "optionsnot" doesn't exist so output is empty
cat quiz.json | jq '.quiz.sport.q1 | keys[] | select(.=="optionsnot")'
```


###
6. To grep for a particular value
```
$ cat quiz.json | jq '.quiz.sport.q1.options[] | select(.=="New York Bulls")'

"New York Bulls"
```


7. To iterate over the list
```
$ cat quiz.json | jq '.quiz.sport.q1.options[0]'

"New York Bulls"
```
> Note: To get all elements, use `options[]`. To get first element, use `options[0]` as so on...


