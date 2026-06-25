Mini Research Proposal
Định lượng độ bất định cho HTE trong vùng kém nhận diện do thiếu modality mang tính thông tin và vi phạm overlap trong EHR đa phương thức

## 1. Động cơ nghiên cứu

Trong y tế, một phương pháp điều trị có thực sự giúp bệnh nhân hay không, và giúp ai nhiều hơn ai.
Để trả lời câu hỏi đó, ta cần ước lượng treatment effect, tức là mức thay đổi ở kết quả điều trị nếu bệnh nhân được điều trị so với nếu không được điều trị. Kết quả điều trị ở đây có thể là tỷ lệ sống sót, mức độ hồi phục, nguy cơ biến chứng, thời gian nằm viện, hoặc một chỉ số sức khỏe nào đó mà bác sĩ quan tâm.

Nếu chỉ nhìn trung bình trên toàn bộ bệnh nhân, ta thu được average treatment effect (ATE), tức là hiệu quả điều trị trung bình của một phương pháp trên cả quần thể. Nhưng trong thực tế, điều trị thường không tác động giống nhau lên mọi người. Có bệnh nhân hưởng lợi nhiều, có người hưởng lợi ít, thậm chí có người có thể bị hại. Vì vậy, điều quan trọng hơn là ước lượng heterogeneous treatment effects (HTE) hoặc conditional average treatment effect (CATE), tức là hiệu quả điều trị riêng cho từng nhóm bệnh nhân hoặc từng kiểu hồ sơ bệnh án khác nhau. => ATE trả lời câu hỏi thuốc này trung bình có hiệu quả không, còn HTE/CATE trả lời câu hỏi thuốc này hiệu quả với ai và trong hoàn cảnh nào.

Bài toán này đặc biệt quan trọng trong dữ liệu electronic health records (EHR) - hồ sơ bệnh án điện tử, nơi mỗi bệnh nhân có thể có nhiều loại dữ liệu khác nhau như xét nghiệm máu, ảnh MRI hoặc CT, ghi chú lâm sàng, tín hiệu monitor, hoặc các thông tin hành chính. Tuy nhiên, trong dữ liệu EHR thực tế, một khó khăn lớn là nhiều bệnh nhân bị thiếu một số loại dữ liệu. Ví dụ, không phải ai cũng có MRI, CT hay xét nghiệm chuyên sâu. Điểm quan trọng là việc thiếu này thường không xảy ra ngẫu nhiên. Một bệnh nhân có được chỉ định chụp MRI hay không có thể phụ thuộc vào mức độ nặng của bệnh, đánh giá của bác sĩ, khả năng chi trả, điều kiện bệnh viện, hoặc hướng điều trị đang được cân nhắc.

Vì vậy, thiếu dữ liệu trong bối cảnh này không chỉ là chuyện thiếu thông tin đầu vào rồi điền giá trị còn thiếu. Nó có thể phản ánh chính quá trình ra quyết định lâm sàng và tình trạng bệnh nhân, nên nếu xử lý không cẩn thận, mô hình có thể rút ra kết luận sai về hiệu quả điều trị. Nói cách khác, việc thiếu MRI hay xét nghiệm không chỉ làm mô hình dự đoán kém chính xác hơn, mà còn có thể làm sai lệch việc ước lượng treatment effect.

Vấn đề này càng nghiêm trọng hơn khi mục tiêu là CATE/HTE chứ không phải chỉ là ATE. Với ATE, ta chỉ cần biết hiệu quả trung bình trên toàn bộ quần thể, nên đôi khi một số vùng dữ liệu xấu vẫn có thể bị triệt tiêu khi tính trung bình. Nhưng với CATE, ta cần biết hiệu quả điều trị trong từng nhóm bệnh nhân cụ thể. Nếu đúng nhóm bệnh nhân đó lại vừa có ít dữ liệu so sánh giữa người được điều trị và không điều trị, vừa có nguy cơ thiếu dữ liệu theo cách có liên quan đến tình trạng bệnh, thì việc ước lượng hiệu quả điều trị cho nhóm đó sẽ trở nên kém tin cậy.

=> tập trung vào một câu hỏi chính: làm thế nào để nhận biết những vùng bệnh nhân mà ước lượng hiệu quả điều trị kém tin cậy vì vừa thiếu dữ liệu so sánh, vừa thiếu các modality quan trọng theo cách không ngẫu nhiên, và làm thế nào để phản ánh sự thiếu tin cậy đó vào uncertainty của mô hình. Mục tiêu không chỉ là dự đoán một con số hiệu quả điều trị, mà còn biết khi nào mô hình nên tự tin và khi nào mô hình nên thừa nhận rằng kết quả ở nhóm bệnh nhân đó chưa đủ đáng tin.

## 2. Câu hỏi nghiên cứu

Câu hỏi trung tâm của đề tài là:

Có thể xác định các vùng bệnh nhân mà ước lượng HTE hoặc CATE đồng thời kém tin cậy do treatment overlap yếu và thiếu modality mang tính thông tin, sau đó hiệu chỉnh hoặc mở rộng uncertainty cho CATE tương ứng để hỗ trợ ra quyết định điều trị an toàn hơn hay không?

Từ đó, đề tài tập trung vào ba câu hỏi con:

- Làm thế nào để phát hiện hoặc định lượng rủi ro missingness mang tính thông tin ở cấp subgroup hoặc vùng covariate trong EHR đa phương thức?
- Làm thế nào để kết hợp rủi ro missingness này với chẩn đoán overlap để xác định các vùng kém nhận diện cho CATE?
- Liệu việc điều chỉnh uncertainty theo mức độ rủi ro cấu trúc này có giúp cải thiện độ tin cậy của HTE và hỗ trợ treatment selection an toàn hơn hay không?

## 2b. 

HTE/CATE uncertainty đã có nhiều hướng như bootstrap, Bayesian, conformal, and uncertainty-aware causal inference.

Overlap/positivity violation là vấn đề đã được nhận diện rất rõ trong causal inference.

## 3. Giả thuyết nghiên cứu

Đề tài đặt ra ba giả thuyết chính.

**H1 — Missing modality trong EHR đa phương thức là tín hiệu cấu trúc chứ không chỉ là nhiễu đo lường.**  
Cụ thể, pattern thiếu modality mang thông tin về severity, clinical workflow hoặc treatment pathway, và do đó có thể tạo ra selection bias hoặc confounding-like bias cho HTE nếu bị bỏ qua hoặc xử lý như missingness thuần túy.

**H2 — Vùng có overlap yếu và missingness mang tính thông tin cao là vùng kém nhận diện nhất đối với CATE.**  
Trong các vùng này, uncertainty của CATE không nên chỉ phản ánh phương sai thống kê thông thường, mà cần phản ánh thêm độ mong manh về nhận diện nhân quả do support yếu và quan sát chọn lọc.

**H3 — Một cơ chế điều chỉnh uncertainty hoặc abstention (từ chối đưa ra quyết định khi rủi ro quá cao) dựa trên overlap và missingness risk sẽ cải thiện độ tin cậy của HTE cho treatment selection.**  
Cụ thể, nếu mô hình nhận diện được các vùng subgroup rủi ro cao và mở rộng khoảng tin cậy, giảm độ tự tin hoặc trì hoãn khuyến nghị điều trị trong các vùng đó, thì hiệu quả ra quyết định điều trị sẽ an toàn và ổn định hơn so với các phương pháp uncertainty thông thường cho HTE.

## 4. Ý tưởng phương pháp

Đề tài đề xuất một framework sơ bộ gồm ba thành phần.

### a) Ước lượng HTE hoặc CATE trên dữ liệu đa phương thức

Sử dụng một hoặc nhiều bộ ước lượng HTE hiện đại làm baseline, ví dụ:

- DR-learner (doubly robust learner, bộ học có tính bền vững kép)
- R-learner
- X-learner
- causal forest
- hoặc một kiến trúc representation learning (học biểu diễn) cho dữ liệu đa phương thức

Mục tiêu ở bước này không phải phát minh estimator mới từ đầu, mà xây dựng một nền HTE đủ mạnh để nghiên cứu uncertainty dưới missing modality.

### b) Xây dựng chỉ số rủi ro cấu trúc cho từng vùng bệnh nhân

Đối với mỗi bệnh nhân hoặc vùng covariate x, tính hai nhóm tín hiệu:

- **Overlap risk**: mức độ yếu của positivity hoặc treatment overlap, ví dụ dựa trên propensity score cực trị, local support, density ratio hoặc các overlap diagnostics ở cấp subgroup.
- **Missingness risk**: mức độ thiếu modality có khả năng mang tính thông tin, ví dụ dựa trên:
  - pattern availability của các modality
  - xác suất một modality bị thiếu có phụ thuộc vào severity proxy, treatment hoặc outcome proxy hay không
  - mức độ khác biệt về phân phối missingness giữa các subgroup lâm sàng

Từ đó, xây dựng một chỉ số tổng hợp cho vùng kém nhận diện theo hai cơ chế đồng thời, kết hợp cả overlap risk và missingness risk.

### c) Điều chỉnh uncertainty theo vùng rủi ro cao

Trên nền uncertainty của estimator HTE, ví dụ bootstrap, conformal prediction hoặc Bayesian bootstrap, đề tài sẽ nghiên cứu cơ chế:

- mở rộng uncertainty intervals trong các vùng có chỉ số rủi ro cấu trúc cao
- hoặc abstention / defer trong treatment recommendation khi mức rủi ro vượt ngưỡng
- hoặc kết hợp uncertainty thống kê với một penalty phản ánh identification fragility (độ mong manh của nhận diện)

Mục tiêu là tạo ra một uncertainty measure không chỉ trả lời mô hình có chắc về mặt thống kê hay không, mà còn phản ánh hiệu ứng này có đáng tin về mặt nhân quả trong vùng bệnh nhân này hay không.

## 5. Kế hoạch đánh giá

Đề tài có thể được đánh giá theo hai tầng.

### i) Đánh giá estimation và uncertainty

- Sai số CATE hoặc PEHE (precision in estimation of heterogeneous effect, sai số trong ước lượng hiệu ứng dị biệt) nếu dùng thiết lập semi-synthetic
- Coverage của confidence interval hoặc predictive interval cho CATE
- Interval width và calibration error theo từng subgroup
- So sánh giữa các vùng overlap tốt và overlap kém, missingness thấp và missingness cao

### ii) Đánh giá decision utility

- Policy value khi dùng HTE để chọn điều trị
- So sánh giữa:
  - policy chỉ dùng point estimate
  - policy dùng uncertainty-aware thresholding
  - policy có abstention hoặc defer ở vùng rủi ro cao
- Đo mức giảm regret hoặc giảm harmful treatment assignment trong các subgroup rủi ro cao

Dữ liệu đánh giá có thể bắt đầu từ:

- **Semi-synthetic benchmark**: tạo outcome và treatment theo cơ chế biết trước, sau đó chủ động can thiệp pattern missing modality theo MCAR, MAR, MNAR hoặc MMNAR để kiểm tra khả năng phục hồi của uncertainty.
- **EHR đa phương thức thực tế** nếu có, nơi availability của imaging, lab hoặc notes khác nhau giữa các bệnh nhân và có khả năng phản ánh clinical workflow.

## 6. Đóng góp kỳ vọng

Nếu thành công, đề tài có thể đóng góp ở ba mức.

**Thứ nhất, đóng góp khái niệm.**  
Đề tài đưa ra một framing rõ ràng rằng missing modality trong EHR đa phương thức không nên được xem thuần túy là bài toán imputation, mà là một phần của causal data-generating process có thể phá vỡ nhận diện HTE ở cấp subgroup.

**Thứ hai, đóng góp phương pháp.**  
Đề tài đề xuất một framework modality-missingness-aware uncertainty quantification cho HTE, trong đó uncertainty được điều chỉnh theo sự kết hợp giữa overlap violation và informative missingness risk.

**Thứ ba, đóng góp ứng dụng.**  
Đề tài cung cấp một cơ chế phát hiện các vùng bệnh nhân mà khuyến nghị điều trị từ mô hình causal nên được giảm độ tự tin, trì hoãn hoặc yêu cầu thêm thông tin, thay vì đưa ra dự đoán HTE với mức chắc chắn không phù hợp.

## 7. Rủi ro và giới hạn

Đề tài này cũng có một số rủi ro quan trọng.

- Khó phân biệt MMNAR thực sự với missingness chỉ phụ thuộc proxy quan sát được, nên cần cẩn trọng khi diễn giải cơ chế nhân quả.
- Non-identifiability dưới MNAR hoặc MMNAR có thể khiến việc sửa hoàn toàn bias là không thể nếu không có giả định bổ sung. Vì vậy, hướng khả thi hơn có thể là uncertainty inflation, sensitivity analysis (phân tích độ nhạy) hoặc partial identification (nhận diện từng phần), thay vì khẳng định point identification.
- Đánh giá trên dữ liệu thật sẽ khó vì ground-truth CATE không quan sát được. Do đó, thiết kế semi-synthetic nhiều khả năng là thành phần bắt buộc.
- Nếu đồng thời ôm cả HTE learning, missingness modeling, overlap-aware uncertainty và decision policy, scope đề tài có thể quá lớn. Vì vậy, giai đoạn đầu nên ưu tiên một phiên bản tối giản gồm: HTE baseline cố định + đo overlap risk + đo missingness risk + uncertainty inflation và evaluation.

## 8. Kết luận ngắn

Đề tài đề xuất nghiên cứu định lượng độ bất định cho HTE trong các vùng bệnh nhân kém nhận diện do đồng thời có treatment overlap yếu và thiếu modality mang tính thông tin trong EHR đa phương thức. Ý tưởng cốt lõi là: với HTE và CATE, missing modality không chỉ làm mất thông tin đầu vào, mà còn có thể phá vỡ nhận diện ở cấp subgroup. Vì vậy, uncertainty cho CATE cần phản ánh không chỉ sai số thống kê mà cả độ mong manh nhân quả do support yếu và quan sát chọn lọc. Nếu làm tốt, đây có thể trở thành một hướng nối giữa causal machine learning, uncertainty quantification và multimodal healthcare theo một cách vừa có chiều sâu phương pháp, vừa có ý nghĩa triển khai thực tế.