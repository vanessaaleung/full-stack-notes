# React Forms, Flow Architecture and Introduction to Redux

1. [Controlled Forms](#controlled-forms)
2. [Controlled Form Validation](#controlled-form-validation)

## Controlled Forms
1. Import components
```javascript
import { Button, Form, FormBroup, Label, Input, Col } from 'reactstrap';
```

2. Set up properties that are linked to the form in state
```javascript
this.state = {
    firstname: '',
    lastname: '',
    telnum: '',
    email: '',
    agree: false,
    contactType: 'Tel.',
    message: ''
}
```
3. Create the form
- `<FormBroup row>`: occupies a row
- `htmlFor="firstname"`: avoid confusion with javascripts' `for`
- `md={10}`: occupies 10 columns
- `name="firstname"`: ties to the Label
- `value={this.state.firstname}`: ties to the state
```jsx
<Form>
    <FormBroup row>
        <Label htmlFor="firstname" md={2}>First Name</Label>
        <Col md={10}>
            <Input type="text" id="firstname" 
                    name="firstname" placeholder="First Name"
                    value={this.state.firstname} />
        </Col>
    </FormBroup>
</Form>
```

4. Handle Submission
- Submit button
```javascript
<Col md={{size: 10, offset: 2}}>
    <Button type="submit" color="primary">
        Send Feedback
    </Button>
</Col>
```
- handleSubmit
  - `event.preventDefault();`: prevent the browser to go to the next page
```javascript
handleSubmit(event) {
    console.log("Current State is: " + JSON.stringify(this.state));
    alert("Current State is: " + JSON.stringify(this.state));
    event.preventDefault();
}
```

- handleInputChange
```javascript
handleInputChange(event) {
    const target = event.target;  // retrieve target input
    const value = target.type === 'checkbox' ? target.checked : target.value;
    const name = target.name; // retrieve field name

    this.setState({
        [name]: value
    })
}
```
- Implement the functions
```jsx
<Form onSubmit={this.handleSubmit}>
```
```jsx
<Input type="text" id="firstname" name="firstname" placeholder="First Name"
        value={this.state.firstname}
        onChange={this.handleInputChange} />
```
- Bind the functions
```javascript
this.handleSubmit = this.handleSubmit.bind(this);
```

## Controlled Form Validation
1. Add `touched` to the state
```javascript
touched: {
    firstname: false,
    lastname: false,
    telnum: false,
    email: false
}
```

2. Add the `handleBlur` method to indicate which field has been modified
```javascript
handleBlur = (field) => (event) => {
    this.setState({
        touched: { ...this.state.touched, [field]: true}
    });
}
```
- Bind the functions
```javascript
this.handleBlur = this.handleBlur.bind(this);
```

3. Implement the `handleBlur` method in each field
```jsx
onBlur={this.handleBlur('firstname')}
```
4.  Add the `validate` method:
```javascript
validate(firstname, lastname, telnum, email) {
    const errors = {
        firstname: '',
        lastname: '',
        telnum: '',
        email: ''
    };

    if (this.state.touched.firstname && firstname.length < 3) {
        errors.firstname = 'First Name should be >= 3 characters';
    }
    else if (this.state.touched.firstname && firstname.length > 10) {
        errors.firstname = 'First Name should be <= 10 characters';
    }
}
```
5. Display the errors in the form
```jsx
<FormFeedback>{errors.firstname}</FormFeedback>
```
6. Set the valid flag for each field
```jsx
valid={errors.firstname === ''}
invalid={errors.firstname !== ''}
```







   