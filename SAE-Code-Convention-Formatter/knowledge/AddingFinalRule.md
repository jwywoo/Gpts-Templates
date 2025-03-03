# Adding Final Rule

## Purpose

All the variables, parameters and arguments in the code should have final unless it violates any syntax.

## Examples

- Before

```java
// ApiResponse.java
@Getter
@AllArgsConstructor
public class ApiResponse<T> {
    private String message;
    private T data;
    private int statusCode;
}

// CompanyRepositoryImpl.java
@Repository
@RequiredArgsConstructor
public class CompanyRepositoryImpl {
    private final CompanyJpaRepository companyJpaRepository;
    public Optional<Company> findByIsuSrtCd(String tickerCode) {
        return companyJpaRepository.findByIsuSrtCd(tickerCode);
    }

}

```

- After

```java
// ApiResponse.java
@Getter
@AllArgsConstructor
public class ApiResponse<T> {
    private final String message;
    private final T data;
    private final int statusCode;
}

// CompanyRepositoryImpl.java
@Repository
@RequiredArgsConstructor
public class CompanyRepositoryImpl {
    private final CompanyJpaRepository companyJpaRepository;
    public Optional<Company> findByIsuSrtCd(String final tickerCode) {
        return companyJpaRepository.findByIsuSrtCd(tickerCode);
    }

}
```
