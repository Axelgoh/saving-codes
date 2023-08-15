
{likedPosts.length > 0 && (
        <div>
          <h2>Your Liked Posts</h2>
          <table>
            <thead>
              <tr>
                <th>Title</th>
                <th>Description</th>
                <th>Likes</th>
              </tr>
            </thead>
            <tbody>
              {likedPosts.map((feedback) => (
                <tr key={feedback.id}>
                  <td>{feedback.title}</td>
                  <td>{feedback.description}</td>
                  <td>{feedback.likes}</td>
                </tr>
              ))}
            </tbody>
          </table>
        </div>
      )}





Table of Contents
Introduction
Features
Getting Started
Prerequisites
Installation
Running the Application
API Endpoints
GET /api/feedbacks
POST /api/feedbacks
PUT /api/feedbacks/{title}/like
DELETE /api/feedbacks
Examples
Contributing
License
Introduction
This REST API provides a platform for managing user feedback entries. It's built using Quarkus framework for Java applications and follows standard REST principles.

Features
Submit new feedback entries.
Retrieve all feedback entries.
Like feedback entries to indicate user preferences.
Delete unwanted feedback entries.
Getting Started
Prerequisites
To run this API locally, you need to have the following installed:

Java Development Kit (JDK) 8 or later
Maven
Git
Installation
Clone the repository:

sh
Copy code
git clone https://github.com/your-username/feedback-api.git
cd feedback-api
Build the application:

sh
Copy code
mvn clean package
Running the Application
Start the Quarkus application:

sh
Copy code
java -jar target/feedback-api.jar
The API will be accessible at http://localhost:8080.

API Endpoints
GET /api/feedbacks
Retrieve a list of all feedback entries.

POST /api/feedbacks
Submit a new feedback entry.

PUT /api/feedbacks/{title}/like
Increment the likes count for a specific feedback entry.

DELETE /api/feedbacks
Delete a feedback entry.

Examples
Here are some examples of how to interact with the API using curl:

sh
Copy code
# Get all feedback entries
curl http://localhost:8080/api/feedbacks

# Submit a new feedback entry
curl -X POST -H "Content-Type: application/json" -d '{"title":"New Feedback", "description":"This is a new feedback."}' http://localhost:8080/api/feedbacks

# Like a feedback entry
curl -X PUT http://localhost:8080/api/feedbacks/New%20Feedback/like

# Delete a feedback entry
curl -X DELETE -H "Content-Type: application/json" -d '{"title":"New Feedba



package org.acme;

public class Feedback {
    public String title;
    public String description;

    public Feedback(String title, String description) {
        this.title = title;
        this.description = description;
    }
}


package org.acme;

import java.util.Collections;
import java.util.LinkedHashMap;
import java.util.Set;

import jakarta.ws.rs.DELETE;
import jakarta.ws.rs.GET;
import jakarta.ws.rs.POST;
import jakarta.ws.rs.Path;

@Path("/feedbacks")
public class FeedbackResource {

    private Set<Feedback> feedbacks = Collections.newSetFromMap(Collections.synchronizedMap(new LinkedHashMap<>()));

    public FeedbackResource() {
        feedbacks.add(new Feedback("Efficiency working", "Implement team bonding every friday to allow team to build strong wokring ties. "));
        feedbacks.add(new Feedback("Vending Machine", "Provide vending machine in the office to allow workers to save time on going out to get snacks and instead go to the vending machine to get their snacks fixed."));
        feedbacks.add(new Feedback("Efficiency working", "Implement team bonding every friday to allow team to build strong wokring ties. "));
        feedbacks.add(new Feedback("Efficiency working", "Implement team bonding every friday to allow team to build strong wokring ties. "));

    }

    @GET
    public Set<Feedback> list() {
        return feedbacks;
    }

    @POST
    public void add(Feedback feedback) {
        feedbacks.add(feedback);
    }

    @DELETE
    public Set<Feedback> delete(Feedback feedback) {
        feedbacks.removeIf(existingFeedback -> existingFeedback.title.contentEquals(feedback.title));
        return feedbacks;
    }
}
// like function below 

const handleLikeFeedback = (title) => {
  fetch(`http://localhost:8080/api/feedbacks/${title}/like`, {
    method: 'PUT',
  })
    .then(() => {
      const updatedFeedbacks = feedbacks.map((feedback) =>
        feedback.title === title ? { ...feedback, likes: feedback.likes + 1 } : feedback
      );
      setFeedbacks(updatedFeedbacks);
    })
    .catch((error) => console.error('Error liking feedback:', error));
};

