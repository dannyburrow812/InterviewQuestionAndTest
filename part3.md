#  Part 3: Practical Coding Challenge
## Task: Modify the UserRepository to include a method that removes a user by ID. Ensure it handles cases where the user does not exist.


To modify the UserRepository to include a method that removes a user by ID and handles cases where the user does not exist, I have added a method RemoveUser as shown below:
```c#
public class UserRepository 
{
    private readonly Dictionary<int, User> _users = new Dictionary<int, User>();

    public User GetUser(int id)
    {
        if (_users.TryGetValue(id, out User user))
        {
            return user;
        }
        return null; // Or throw an exception indicating user not found.
    }

    public void AddUser(User user)
    {
        if (user == null)
        {
            throw new ArgumentNullException(nameof(user));
        }

        lock (_users)
        {
            if (!_users.ContainsKey(user.Id))
            {
                _users.Add(user.Id, user);
            }
            else
            {
                // Handle duplicate user ID scenario, throw exception or log.
            }
        }
    }

    public bool RemoveUser(int id)
    {
        lock (_users)
        {
            if (_users.ContainsKey(id))
            {
                _users.Remove(id);
                return true;
            }
            return false; // User with the given ID does not exist.
        }
    }
}

```
