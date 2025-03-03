# Comment Rule

## Purpose

Comments should provide details but got to be compact. It should not include any unnecessary information.

## Examples

- Before

```java
public ResponseEntity<ApiResponse<List<SavedStockResponseDto>>> stockGet(Member member) {

    List<SavedStock> savedStockList = savedStockJpaRepository.findAllByMember(member).orElseThrow(
            () -> new ResourceNotFoundException("유효하지않은 정보입니다.")
    );

    List<SavedStockResponseDto> savedStockResponseDtoList = savedStockList.stream()
            .filter(savedStock -> savedStock.getDeletedDateTime() == null)
            .map(savedStock -> new SavedStockResponseDto(
                    savedStock.getId(),
                    savedStock.getCompany().getIsuSrtCd(),
                    savedStock.getCompany().getIsuNm()
            ))
            .toList();

    return ResponseEntity.status(HttpStatus.OK)
            .body(new ApiResponse<>(
                    "조회 성공",
                    savedStockResponseDtoList,
                    HttpStatus.OK.value()
            ));
}
```

- After

```java
/**
 * Getting list of stock saved by the member
 *
 * @param member: Member for filtering out
 * @return ON Success list of saved stocks
 */
public ResponseEntity<ApiResponse<List<SavedStockResponseDto>>> stockGet(Member member) {

    List<SavedStock> savedStockList = savedStockJpaRepository.findAllByMember(member).orElseThrow(
            () -> new ResourceNotFoundException("유효하지않은 정보입니다.")
    );

    List<SavedStockResponseDto> savedStockResponseDtoList = savedStockList.stream()
            .filter(savedStock -> savedStock.getDeletedDateTime() == null)
            .map(savedStock -> new SavedStockResponseDto(
                    savedStock.getId(),
                    savedStock.getCompany().getIsuSrtCd(),
                    savedStock.getCompany().getIsuNm()
            ))
            .toList();

    return ResponseEntity.status(HttpStatus.OK)
            .body(new ApiResponse<>(
                    "조회 성공",
                    savedStockResponseDtoList,
                    HttpStatus.OK.value()
            ));
}
```
