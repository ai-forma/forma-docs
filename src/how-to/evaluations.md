# Testing and Evaluation


## Running evaluations 

### In development

At the moment, we use [Arize Phoenix](https://phoenix.arize.com/) as an evaluation platform. 


```sh
docker run  --rm -p 6006:6006 -p 4317:4317 -i -t arizephoenix/phoenix:latest
```

### In production

> This section is not yet written



# Evaluate your First Agent

Eval templates allow for the following inputs:

* `input`
* `actual_output`
* `expected_output`

And they will try to generate

* `label`
* `score`
* `explanation`