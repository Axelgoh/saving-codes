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

