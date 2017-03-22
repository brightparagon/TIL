# How does a child component communicate with its parent component?
Sometimes it happens to update the state of a parent component from a child component.

### Let's take an example right away

Let's say there's a List component that outputs a list of postings. And there is a
Post component that is going to be made numerously and rendered in the List component. If an user click one posting in the List page, the List component shows that posting. In this case
the List component has postings data from somewhere like its parent or data-fetch with AJAX.
And it has a state for one posting to show when an user clicks it. So, the state of the List
component needs to be updated by the Post component that is clickable. Maybe this scenario
doesn't explain well this concept but it's an example to show how it works!

Here is the Post component below.
```javascript
import React from 'react';

class Post extends React.Component {
  constructor(props) {
    super(props);
  }

  render() {
    return(
      <div className="Post">
        <Button>
          {this.props.data.title}
        </Button>
      </div>
    );
  }
}

Post.propTypes = {
  data: React.PropTypes.object
};

Post.defaultProps = {
  data: {
    _id: 'id012345',
    title: 'title',
    contents: 'contents'
  }
};

export default Post;
```

There is no function for handling buttons right now. If a button is clicked it
should send its post data for the List component to show it. So, this child component
communicates with its parent component using a function for clicks.

And here is the List component below. Let's assume that it takes posts data from its parent.
```javascript
import React from 'react';
import {Post} from './';

class List extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      post: {
        _id: '',
        title: '',
        contents: ''
      },
    };
  }

  render() {
    const posts = this.props.posts.map((post, i) =>
      <div>
        <br/>
        <Post key={post._id} data={post}/>
      </div>
    );

    return(
      <div className="List">
        {posts}
      </div>
    );
  }
}

List.propTypes = {
  posts: React.PropTypes.array
};

List.defaultProps = {
  posts: []
};

export default List;
```

So, where would be a good place to make a fuction for communication? Since there is no
upwards data flow in React, it would be reasonable to make it in the parent component.

Let's modify our parent component like below.
```javascript
// ...
class List extends React.Component {
  constructor(props) {
    // ...
    this.state = {
      post: {
        _id: '',
        title: '',
        contents: ''
      },
    };
    this.handleShow = this.handleShow.bind(this);
  }

  handleShow(post) {
    this.setState({
      post: post
    });
  }

  render() {
    const posts = this.props.posts.map((post, i) =>
      <div>
        <br/>
        <Post key={post._id} data={post} onShow={this.handleShow}/>
      </div>
    );
    // ...
  }
}
```

The handleShow function is delivered down to its child component so that it can
change its state to show a post.

It's time to modify our child component like below.
```javascript
// ...
class Post extends React.Component {
  constructor(props) {
    // ...
    this.handleShow = this.handleShow.bind(this);
  }

  handleShow() {
    this.props.onShow(this.props.data);
  }

  render() {
    return(
      <div className="Post">
        <Button onClick={this.handleShow}>
          {this.props.data.title}
        </Button>
      </div>
    );
  }
}
// ...
```

Now it's ready to update the state(post data) of the List component from the
Post component. Conclusively, if a parent should update its state depending on its
child's behavior, functions to update the state of a parent component are good to be
placed in a parent component and delivered down to a child component so that a child
component can use it.

### Reference
https://discuss.reactjs.org/t/is-this-a-decent-pattern-to-update-parent-state-from-children/560

http://stackoverflow.com/questions/35537229/how-to-update-parents-state-in-react

http://stackoverflow.com/questions/40086451/react-update-state-in-parent-from-child-components
