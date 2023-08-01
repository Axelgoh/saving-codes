Create a Java class named Feedback to represent the feedback entity. It should contain fields for id, feedback, and feedbackDescription.
java
Copy code
import javax.persistence.*;

@Entity
@Table(name = "feedbacks") // Replace "feedbacks" with the actual table name in the PostgreSQL database
public class Feedback {

    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;

    @Column(nullable = false)
    private String feedback;

    @Column(nullable = false)
    private String feedbackDescription;

    // Constructors, getters, setters, etc.
}


Create a Java interface named FeedbackRepository to define the repository methods for handling database interactions.
java
Copy code
import javax.transaction.Transactional;
import java.util.List;
import java.util.Optional;

public interface FeedbackRepository {

    List<Feedback> getAllFeedbacks();

    Optional<Feedback> getFeedbackById(Long id);

    Feedback createFeedback(Feedback feedback);

    Feedback updateFeedback(Feedback feedback);

    void deleteFeedback(Long id);
}


Create a class named FeedbackRepositoryImpl that implements the FeedbackRepository interface. This class will handle the database interactions with PostgreSQL.
java
Copy code
import io.quarkus.hibernate.orm.panache.PanacheRepository;

import javax.enterprise.context.ApplicationScoped;
import javax.transaction.Transactional;
import java.util.List;
import java.util.Optional;

@ApplicationScoped
@Transactional
public class FeedbackRepositoryImpl implements FeedbackRepository, PanacheRepository<Feedback> {

    @Override
    public List<Feedback> getAllFeedbacks() {
        return findAll().list();
    }

    @Override
    public Optional<Feedback> getFeedbackById(Long id) {
        return findByIdOptional(id);
    }

    @Override
    public Feedback createFeedback(Feedback feedback) {
        persist(feedback);
        return feedback;
    }

    @Override
    public Feedback updateFeedback(Feedback feedback) {
        return getFeedbackById(feedback.getId())
                .map(existingFeedback -> {
                    existingFeedback.setFeedback(feedback.getFeedback());
                    existingFeedback.setFeedbackDescription(feedback.getFeedbackDescription());
                    persist(existingFeedback);
                    return existingFeedback;
                })
                .orElse(null);
    }

    @Override
    public void deleteFeedback(Long id) {
        getFeedbackById(id).ifPresent(this::delete);
    }
}


Create a class named FeedbackResource to define the RESTful endpoints for the feedbacks resource. Use JAX-RS annotations to map the methods to HTTP endpoints.
java
Copy code
import javax.inject.Inject;
import javax.ws.rs.*;
import javax.ws.rs.core.MediaType;
import java.util.List;
import java.util.Optional;

@Path("/api/feedbacks")
@Produces(MediaType.APPLICATION_JSON)
@Consumes(MediaType.APPLICATION_JSON)
public class FeedbackResource {

    @Inject
    FeedbackRepository feedbackRepository;

    @GET
    public List<Feedback> getAllFeedbacks() {
        return feedbackRepository.getAllFeedbacks();
    }

    @GET
    @Path("/{id}")
    public Feedback getFeedbackById(@PathParam("id") Long id) {
        return feedbackRepository.getFeedbackById(id).orElse(null);
    }

    @POST
    public Feedback createFeedback(Feedback feedback) {
        return feedbackRepository.createFeedback(feedback);
    }

    @PUT
    @Path("/{id}")
    public Feedback updateFeedback(@PathParam("id") Long id, Feedback feedback) {
        feedback.setId(id);
        return feedbackRepository.updateFeedback(feedback);
    }

    @DELETE
    @Path("/{id}")
    public void deleteFeedback(@PathParam("id") Long id) {
        feedbackRepository.deleteFeedback(id);
    }
}
