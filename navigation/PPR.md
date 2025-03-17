---
layout: page
title: PPR Blog
permalink: /PPR/
---


#### What is PPR?

- A personal project reference refers to a specific project that a student has worked on, typically as part of their Create Performance Task. This reference is used to explain programming concepts, algorithms, and abstractions in relation to a project the student has personally developed.

- Students have to write a program, a video demonstration of the code (1 minute max), and a written response explaining their code. 

- Written Part is 4 questions that students have to answer after the MCQ for 1 hour

- Students often need to refer to a personal project to illustrate their understanding of computing principles. This could be a program, app, or game they coded during the course.

#### Requirements for the PPR

- Submit 2 sections
- Must demonstrate a procedure: 1 with a parameter and a list with its usage 
- Must include sequencing, selection, and iteration 
- CPT Requirements are used in the PPR



#### How my feature is related to PPR:


#### User Input

```python
def post(self):
    # Obtain the request data sent by the RESTful client API
    data = request.get_json()
    # Create a new post object using the data from the request
    post = BinaryConverter(data['binary'], data['decimal'])
    # Save the post object using the Object Relational Mapper (ORM) method defined in the model
    post.create()
    # Return response to the client in JSON format, converting Python dictionaries to JSON format
    return jsonify(post.read())

```
- The post method allows users to input data in JSON format (binary and decimal values) through an API request, fulfilling the User Input requirement.

#### Iteration

```python
def get(self):
    try:
        # Query all entries in the BinaryHistory table
        entries = BinaryConverter.query.all()
        # Convert the entries to a list of dictionaries
        results = [entry.read() for entry in entries]
        # Return the list of results in JSON format
        return jsonify(results)
    except Exception as e:
        # Return an error message in case of failure
        return jsonify({"error": str(e)}), 500

```

- This get method uses iteration ([entry.read() for entry in entries]) to process multiple database entries, satisfying the Processing (Iteration) requirement.

#### Lists and Data Storage 

```python

let conversionHistory = [];

function convertToBinary(decimalNumber) {
    if (isNaN(decimalNumber) || decimalNumber < 0) {
        return "Please enter a valid number!";
    }
    const binary = decimalNumber.toString(2);
    conversionHistory.push({decimal: decimalNumber, binary: binary});
    return binary;
}

```

- The game could use a list (array) to store previous binary conversions, user scores, or even difficulty levels.
- The stored data (conversion history) could be used to show the user their past inputs and conversions, or you could display a list of their scores/challenges completed.


#### Parameters

```python

function convertToBinary(decimalNumber) {
    // Check if decimalNumber is valid
    if (isNaN(decimalNumber) || decimalNumber < 0) {
        return "Please enter a valid number!";
    }
    return decimalNumber.toString(2);
}

```

- You could pass the decimal number directly into the function instead of reading it from the DOM, which would make the function more flexible and reusable.

- The function is responsible for converting the decimal number (from input) to binary, and the output (binary value) is displayed on the webpage. This procedure directly addresses 1+ parameters affecting the functionality.


#### Use of Dictionares 
- Stores Data in an Organized Way: Each database entry is converted into a dictionary, where column names (like "id", "binary", and "decimal") act as keys, and the actual data are the values.

- Makes API Responses Easy to Use: Since APIs typically send and receive JSON, which is just a formatted dictionary, converting database entries into dictionaries ensures the data is structured and readable.

- Helps with Data Processing: Dictionaries make it easy to access, modify, and send data, allowing the frontend or other parts of the app to work with structured information efficiently.

``` python 
results = [entry.read() for entry in entries]  # Converts rows into dictionaries
```


<script src="https://utteranc.es/client.js"
        repo="rc765445/rutvik_2025"
        issue-term="pathname"
        theme="github-light"
        crossorigin="anonymous"
        async>
</script>