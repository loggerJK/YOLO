- PyTorch
  - Training Loop 안에서는 항상 파이썬 자체의 자료형(int, float...)이 아닌 torch.Tensor가 사용되어야 한다. 예를 들어, ```target_value = 0```와 같이 선언해주면 loss를 계산할 때 pytorch가 해당 value 때문에 오류를 일으키는 경우가 있다. 앞서 말한 코드는 ```target_value = torch.Tensor([0,])```와 같이 사용해야 pytorch가 잘 작동한다.
  - ```a leaf Variable that requires grad is being used in an in-place operation.``` 에러
    - ```loss = loss + something_else```와 같은 코드 때문에 생기는 에러이다. ```loss_ = loss + something_else```와 같이 in-place operation을 변경해주면 해결이 된다.
  - ```RuntimeError: one of the variables needed for gradient computation has been modified by an inplace operation``` ![https://nieznanm.medium.com/runtimeerror-one-of-the-variables-needed-for-gradient-computation-has-been-modified-by-an-inplace-85d0d207623] 
  - ```loss = torch.sum(torch.cat(loss_list))``` torch.cat을 써야 오류가 안난다
  - opencv의 `im.read()`로 불러들인 이미지는 numpy array로 저장된다.
  - Loss는 CPU에서 계산하는 것이 훨씬 이득이다. 특히 이렇게 for문으로 돌리는 경우라면!
  - `x += y`is inplace. ` x = x + y` is not inplace. PyTorch에서 inplace 연산은 되도록 피해야 한다.
  - `torch.Tensor`는 기본적으로 immutable. 일반적인 경우, 텐서 간의 복사는 복사된 참조 변수의 수정이 기존 참조 변수의 값에 똑같은 영향을 미친다
    - [Tensor element를 mutable하게 복사하기](https://froggydisk.github.io/fourth-post/)