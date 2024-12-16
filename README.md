# Sample Hardhat Project

This project demonstrates a basic Hardhat use case. It comes with a sample contract, a test for that contract, and a Hardhat Ignition module that deploys that contract.

Try running some of the following tasks:

```shell
npx hardhat help
npx hardhat test
REPORT_GAS=true npx hardhat test
npx hardhat node
npx hardhat ignition deploy ./ignition/modules/Lock.js
```

# My Knowledge

- Cài NodeJS vì hardhat là 1 script được tạo từ JS và lưu ở NPM

- có thể cài các thư viện
  `npm install -g truffle` : phát triển dApps

- Tạo folder

- Init git tự động hoặc bỏ -y nếu thủ công

  `npm init -y`

- Cài đặt hardhat : tool đa chức năng, có thể biên dịch, deploy

  `npm install --save-dev hardhat`

# Research

- Keyword

  ```
  abstract
  after
  alias
  apply
  auto
  case
  catch
  copyof
  default
  define
  final
  immutable
  implements
  in
  inline
  let
  macro
  match
  mutable
  null
  of
  override
  partial
  promise
  reference
  relocatable
  sealed
  sizeof
  static
  supports
  switch
  try
  typedef
  typeof
  unchecked
  ```

- Có 3 kiểu biến:

  - `State`: biến bên trong contract
  - `Local`: biến bên trong hàm
  - `Global`: biến global của solidity

- Có 3 loại phạm vi truy cập của biến:

  - `Public`: Biến public có thể được truy cập từ bên ngoài hợp đồng

    Được sử dụng khi bạn muốn một biến hoặc hàm có thể được truy cập công khai bởi bất kỳ ai.

  - `Internal`: _*MẶC ĐỊNH*_

    Chỉ có thể truy cập trong hợp đồng hiện tại và các hợp đồng kế thừa (child contracts). Không thể truy cập từ bên ngoài hợp đồng thông minh.

    Dùng khi bạn muốn giới hạn quyền truy cập chỉ trong hợp đồng hiện tại và hợp đồng kế thừa (dùng trong các hợp đồng con, ví dụ khi kế thừa hợp đồng khác).

  - `Private`:

    Chỉ có thể truy cập trong hợp đồng hiện tại. Không thể truy cập từ hợp đồng kế thừa hoặc từ bên ngoài hợp đồng.

    Dùng khi bạn muốn giữ giá trị hoặc hàm chỉ có thể truy cập trong chính hợp đồng đó, không cho phép kế thừa hay truy cập từ hợp đồng con.

- Các từ khóa khai báo hàm:

  - `public`: Chỉ định hàm có thể được gọi từ bất kỳ đâu (bên trong hợp đồng, từ các hợp đồng khác, hoặc từ các ứng dụng bên ngoài).
  - `internal`: Chỉ định hàm có thể được gọi chỉ trong hợp đồng hiện tại và các hợp đồng kế thừa (subclass).
  - `private`: Chỉ định hàm chỉ có thể được gọi bên trong hợp đồng hiện tại (không thể kế thừa hoặc gọi từ các hợp đồng khác).
  - `external`: Chỉ định hàm có thể được gọi từ các hợp đồng khác hoặc từ bên ngoài, nhưng không thể gọi trực tiếp từ bên trong hợp đồng hiện tại.
  - `view`: Chỉ định hàm không thay đổi trạng thái của hợp đồng và chỉ đọc dữ liệu (không ghi vào blockchain).
  - `pure`: Chỉ định hàm không thay đổi trạng thái và **KHÔNG ĐỌC** trạng thái hợp đồng. Nó chỉ tính toán giá trị dựa trên các đối số và trả về kết quả.
  - `payable`: Chỉ định hàm có thể nhận ether (ví dụ: khi chuyển tiền vào hợp đồng).
  - `constructor`: Hàm khởi tạo hợp đồng, được gọi một lần duy nhất khi hợp đồng được triển khai. Không có kiểu trả về và không thể gọi trực tiếp.
  - `fallback`: Hàm đặc biệt được gọi khi hợp đồng nhận ether mà không có hàm phù hợp để gọi, hoặc khi có dữ liệu không nhận diện được.
  - `receive`: Hàm đặc biệt được gọi khi hợp đồng nhận ether mà không có dữ liệu, và chỉ có thể nhận ether mà không có dữ liệu.

- Có 3 nơi lưu trữ giá trị của biến:

  - `storage` (Bộ nhớ lưu trữ lâu dài)

    - Đặc điểm:

      Lưu trữ dữ liệu trên blockchain (vĩnh viễn).

      Dữ liệu ở đây sẽ không bị mất đi sau khi giao dịch kết thúc.
      Thích hợp cho các biến trạng thái (state variables) của hợp đồng.
      Chi phí lưu trữ trong storage rất cao.

    - Khi nào sử dụng:

      Biến lưu trạng thái (state variables) của hợp đồng.
      Dữ liệu cần được lưu trữ vĩnh viễn trên blockchain.

  - `memory` (Bộ nhớ tạm thời)

    - Đặc điểm:

      Lưu trữ dữ liệu chỉ trong thời gian chạy của hàm.
      Dữ liệu trong memory sẽ bị xóa khi hàm kết thúc.
      Thường được sử dụng cho các biến cục bộ trong hàm, đặc biệt là dữ liệu phức tạp (structs, arrays, mappings).
      Chi phí lưu trữ rẻ hơn so với storage.

    - Khi nào sử dụng:

      Dữ liệu tạm thời chỉ cần trong thời gian chạy hàm.
      Dữ liệu không cần được lưu trữ vĩnh viễn trên blockchain.

  - `calldata` (Dữ liệu chỉ đọc từ input của hàm)

    - Đặc điểm:

      Chỉ được sử dụng cho tham số truyền vào các hàm external.
      Dữ liệu trong calldata không thể thay đổi (immutable).
      Tiết kiệm chi phí gas hơn memory vì nó chỉ là tham chiếu (reference) mà không sao chép dữ liệu.

    - Khi nào sử dụng:

      Dữ liệu chỉ đọc (không thay đổi) được truyền vào một hàm từ bên ngoài hợp đồng.
      Ví dụ: mảng hoặc chuỗi ký tự được truyền làm tham số.

- Các kiểu dữ liệu:

  - Kiểu dữ liệu giá trị:

    - `uint`: số nguyên không âm

      Các kiểu phạm vi uint8/16/32/64/128/256 có các phạm vi giá trị khác nhau.

      Nếu không khai báo số thì sẽ là mặc định phạm vi lớn nhất

    - `int`: số nguyên có dấu
    - `bytes`: Kích thước cố định: bytes1, bytes2, ..., bytes32.

      **_Ba loại trên có thể khai báo số để chỉ định kích thước đầu vào_**

    - `bool`
    - `address`: ethereum 20 bytes (Có thể sử dụng các phương thức như balance hoặc transfer.)

    - `string`
    - `enum`

  - Kiểu dữ liệu tham chiếu:

    - `arrays`
    - `struct`: tập hợp biến giống object JS
    - `mapping`

  - Kiểu dữ liệu đặc biệt:

    - `function`
    - `tuple`

  - Kiểu dữ liệu mặc định có giá trị khi khởi tạo:
    - `uint` và int: 0
    - `bool`: false
    - `address`: 0x0000000000000000000000000000000000000000
    - `string` và bytes: ""

