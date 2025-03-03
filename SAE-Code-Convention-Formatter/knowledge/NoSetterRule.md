# No Setter Rule

## Purpose

No @Setter for any case.

## Examples

- Before

```java
// Member.java
@Entity
@Getter
@Setter
@SuperBuilder
@NoArgsConstructor(access = AccessLevel.PROTECTED)
@AllArgsConstructor
@Slf4j
public class Member extends BaseEntity {
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    @Column(name = "member_id")
    private Long id;

    @Column(nullable = false, unique = true)
    private String googleId;

    @Column(nullable = false, unique = true)
    private String username;

    @Column(nullable = false, unique = true)
    private String email;

    @Column(nullable = false)
    @Enumerated(value = EnumType.STRING)
    private MemberRoleEnum role;

    public Member(String googleId, String email, MemberRoleEnum role) {
        this.googleId = googleId;
        this.email = email;
        this.username = parseUsernameFromEmail(email); // Extract username from email
        this.role = role != null ? role : MemberRoleEnum.USER;
    }

    private String parseUsernameFromEmail(String email) {
        return email.substring(0, email.indexOf('@')); // Extract part before '@'
    }
}

```

- After

```java
// Member.java
@Entity
@Getter
@SuperBuilder
@NoArgsConstructor(access = AccessLevel.PROTECTED)
@AllArgsConstructor
@Slf4j
public class Member extends BaseEntity {
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    @Column(name = "member_id")
    private Long id;

    @Column(nullable = false, unique = true)
    private String googleId;

    @Column(nullable = false, unique = true)
    private String username;

    @Column(nullable = false, unique = true)
    private String email;

    @Column(nullable = false)
    @Enumerated(value = EnumType.STRING)
    private MemberRoleEnum role;

    public Member(String googleId, String email, MemberRoleEnum role) {
        this.googleId = googleId;
        this.email = email;
        this.username = parseUsernameFromEmail(email); // Extract username from email
        this.role = role != null ? role : MemberRoleEnum.USER;
    }

    private String parseUsernameFromEmail(String email) {
        return email.substring(0, email.indexOf('@')); // Extract part before '@'
    }
}
```
