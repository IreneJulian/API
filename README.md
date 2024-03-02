import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;
import org.springframework.web.bind.annotation.*;

import java.util.HashMap;
import java.util.Map;

@SpringBootApplication
@RestController
@RequestMapping("/api")
public class MyApiApplication {

    private Map<Integer, String> users = new HashMap<>();

    public static void main(String[] args) {
        SpringApplication.run(MyApiApplication.class, args);
    }

    @PostMapping("/user")
    public String createUser(@RequestParam int id, @RequestParam String name) {
        users.put(id, name);
        return "User created successfully!";
    }

    @GetMapping("/user/{id}")
    public String getUser(@PathVariable int id) {
        return users.getOrDefault(id, "User not found");
    }

    @DeleteMapping("/user/{id}")
    public String deleteUser(@PathVariable int id) {
        users.remove(id);
        return "User deleted successfully!";
    }
}
