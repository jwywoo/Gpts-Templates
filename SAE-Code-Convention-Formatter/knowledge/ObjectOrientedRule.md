# Object Oriented Rule

## Purpose

Make sure an object to handle it's related task to be oriented.

## Examples

- Before

```java
// SavedStockService.java
@Service
@RequiredArgsConstructor
public class SavedStockService {
    ...
    private SavedStock findByIdSavedStockAuthCheck(Long memberId, Long savedStockId) {
            SavedStock savedStock = savedStockJpaRepository.findById(savedStockId).orElseThrow(() -> new ResourceNotFoundException("유효하지 않은 정보입니다."));
            if (!savedStock.getMember().getId().equals(memberId) || savedStock.isDeleted())
                throw new NotAuthorizedException("잘못된 요청입니다.");
            return savedStock;
    }
}

// SavedStock.java
public class SavedStock extends BaseEntity {

    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    @Column(name = "saved_stock_id")
    private Long id;

    @ManyToOne(fetch = LAZY)
    @JoinColumn(name = "member_id", nullable = false)
    private Member member;

    @ManyToOne(fetch = LAZY)
    @JoinColumn(name = "company_id", nullable = false)
    private Company company;

    @Column(nullable = false)
    private String context;
}
```

- After

```java
// SavedStockService.java
@Service
@RequiredArgsConstructor
public class SavedStockService {
    ...
    private SavedStock findByIdSavedStockAuthCheck(Long memberId, Long savedStockId) {
            SavedStock savedStock = savedStockJpaRepository.findById(savedStockId).orElseThrow(() -> new ResourceNotFoundException("유효하지 않은 정보입니다."));
            if (!savedStock.isOwned(memberId) || savedStock.isDeleted())
                throw new NotAuthorizedException("잘못된 요청입니다.");
            return savedStock;
    }
}

// SavedStock.java
public class SavedStock extends BaseEntity {

    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    @Column(name = "saved_stock_id")
    private Long id;

    @ManyToOne(fetch = LAZY)
    @JoinColumn(name = "member_id", nullable = false)
    private Member member;

    @ManyToOne(fetch = LAZY)
    @JoinColumn(name = "company_id", nullable = false)
    private Company company;

    @Column(nullable = false)
    private String context;

    public boolean isOwned(Long givenId) {
        return this.member.id == givenId
    }
}
```
