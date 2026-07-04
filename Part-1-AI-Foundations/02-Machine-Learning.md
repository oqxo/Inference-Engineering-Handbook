# 02. Machine Learning

Machine learning is a way to build software by learning from examples.

In traditional software, developers write rules. In machine learning, developers provide data, choose a model type, train it, and evaluate how well it performs.

Imagine you want software to detect whether an email is spam. You could try to write rules by hand:

```text
if subject contains "free money", mark as spam
```

That approach breaks quickly because real emails vary. A machine learning system can learn from many examples of spam and non-spam emails. It finds patterns that would be hard to list manually.

## Training Data

Training data is the set of examples used to teach the model. Each example usually contains an input and the expected output.

For spam detection:

- Input: email text
- Expected output: spam or not spam

The quality of the data matters. Bad data leads to bad behavior. Missing examples lead to weak performance in those situations.

## Prediction

After training, the model can make predictions on new inputs. This is inference.

For developers, this looks like calling a function:

```text
prediction = model(input)
```

The important difference is that the function was not written line by line. It was learned from data.

## Why It Matters For Inference

Inference engineers usually do not train the model from scratch. They serve models that already exist. Still, they must understand the basics because model behavior depends on training data, model size, architecture, and evaluation.

When a model gives a strange answer, the cause may not be the server. It may be the model's learned behavior.

## Key Ideas

- Machine learning creates behavior from examples.
- The model learns patterns, not explicit rules.
- Training data quality affects production behavior.
- Inference is the act of using the trained model.

## Developer Checklist

- Ask what data the model was trained or tuned on.
- Test with examples from your real product.
- Do not assume the model understands intent like a human.
- Separate model quality issues from infrastructure issues.

