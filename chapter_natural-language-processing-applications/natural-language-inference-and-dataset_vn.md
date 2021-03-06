<!-- ===================== Bắt đầu dịch Phần 1 ==================== -->
<!-- ========================================= REVISE - BẮT ĐẦU =================================== -->

<!--
# Natural Language Inference and the Dataset
-->

# *Suy diễn Ngôn ngữ tự nhiên và tập dữ liệu*
:label:`sec_natural-language-inference-and-dataset`


<!--
In :numref:`sec_sentiment`, we discussed the problem of sentiment analysis.
This task aims to classify a single text sequence into predefined categories, such as a set of sentiment polarities.
However, when there is a need to decide whether one sentence can be inferred form another, 
or eliminate redundancy by identifying sentences that are semantically equivalent, knowing how to classify one text sequence is insufficient.
Instead, we need to be able to reason over pairs of text sequences.
-->

Trong :numref:`sec_sentiment`, chúng ta đã thảo luận về bài toán phân tích sắc thái. Mục đích của bài toán là phân loại chuỗi văn bản vào các loại đã định trước, chẳng hạn như các sắc thái đối lập. Tuy nhiên, trong trường hợp cần xác định liệu một câu có suy ra được được từ một câu khác không, hoặc cân loại bỏ sự dư thừa bằng việc xác định các câu tương đương về ngữ nghĩa, việc phân lớp một chuỗi văn bản là không đủ. Chúng ta cần phải suy diễn trên một cặp chuỗi văn bản.


<!--
## Natural Language Inference
-->

## *Suy diễn Ngôn ngữ tự nhiên*

<!--
*Natural language inference* studies whether a *hypothesis* can be inferred from a *premise*, where both are a text sequence.
In other words, natural language inference determines the logical relationship between a pair of text sequences.
Such relationships usually fall into three types:
-->

*Suy diễn Ngôn ngữ tự nhiên* nghiên cứu liệu một *giả thuyết* có thể được suy ra được từ một *tiên đề* không, khi cả hai là một chuỗi văn bản. Nói cách khác, suy diễn ngôn ngữ tự nhiên quyết định mối quan hệ logic giữa một cặp chuỗi văn bản. Các mối quan hệ đó thường rơi vào một trong ba loại sau:


<!--
* *Entailment*: the hypothesis can be inferred from the premise.
* *Contradiction*: the negation of the hypothesis can be inferred from the premise.
* *Neutral*: all the other cases.
-->

* *Kéo theo*: Giả thuyết có thể suy ra được từ tiên đề.
* *Đối lập*: Phủ định của giả thuyết có thể suy ra được từ tiên đề.
* *Trung tính*: tất cả các trường hợp khác.


<!--
Natural language inference is also known as the recognizing textual entailment task.
For example, the following pair will be labeled as *entailment* because "showing affection" 
in the hypothesis can be inferred from "hugging one another" in the premise.
-->

Suy diễn ngôn ngữ tự nhiên còn gọi là bài toán nhận dạng quan hệ kéo theo trong văn bản.
Ví dụ, cặp sau được gán nhãn là *kéo theo* bởi vì "thể hiện tình cảm" trong giả thuyết có thể
được suy ra từ "ôm nhau" trong tiên đề.


<!--
> Premise: Two women are hugging each other.
-->

> Tiên đề: Hai người phụ nữ đang ôm nhau.

<!--
> Hypothesis: Two women are showing affection.
-->

> Giả thuyết: Hai người phụ nữ đang thể hiện tình cảm.


<!--
The following is an example of *contradiction* as "running the coding example" indicates "not sleeping" rather than "sleeping".
-->

Sau đây là một ví dụ về *đối lập* bởi vị "chạy đoạn mã ví dụ" cho biết "không ngủ" chứ không phải "ngủ".


<!--
> Premise: A man is running the coding example from Dive into Deep Learning.
-->

> Tiên đề: Một người đàn ông đang chạy đoạn mã ví dụ trong Đắm mình vào học sâu.

<!--
> Hypothesis: The man is sleeping.
-->

> Giả thuyết: Người đàn ông đang ngủ.


<!--
The third example shows a *neutrality* relationship because neither "famous" nor "not famous" can be inferred from the fact that "are performing for us". 
-->

Ví dụ thứ ba cho thấy mối quan hệ *trung tính* vì cả "nổi tiếng" và "không nổi tiếng" đều không thể được suy ra từ thực tế là "đang biểu diễn cho chúng tôi".


<!--
> Premise: The musicians are performing for us.
-->

> Tiên đề: Các nhạc công đang biểu diễn cho chúng tôi.

<!--
> Hypothesis: The musicians are famous.
-->

> Giả thuyết: Các nhạc công là nổi tiếng.


<!--
Natural language inference has been a central topic for understanding natural language.
It enjoys wide applications ranging from information retrieval to open-domain question answering.
To study this problem, we will begin by investigating a popular natural language inference benchmark dataset.
-->

Suy luận ngôn ngữ tự nhiên đã là một chủ đề trung tâm để hiểu ngôn ngữ tự nhiên.
Nó có nhiều ứng dụng khác nhau, từ truy xuất thông tin đến trả lời câu hỏi miền mở.
Để nghiên cứu vấn đề này, chúng ta sẽ bắt đầu bằng cách điều tra tập dữ liệu benchmark phổ biến của suy luận ngôn ngữ tự nhiên.

<!-- ===================== Kết thúc dịch Phần 1 ===================== -->

<!-- ===================== Bắt đầu dịch Phần 2 ===================== -->

<!--
## The Stanford Natural Language Inference (SNLI) Dataset
-->

## Tập dữ liệu Suy diễn ngôn ngữ tự nhiên Stanford (SNLI)


<!--
Stanford Natural Language Inference (SNLI) Corpus is a collection of over $500,000$ labeled English sentence pairs :cite:`Bowman.Angeli.Potts.ea.2015`.
We download and store the extracted SNLI dataset in the path `../data/snli_1.0`.
-->

Corpus suy diễn ngôn ngữ tự nhiên Stanford (SNLI) là một tập hợp hơn $500,000$ cặp câu tiếng Anh được gán nhãn :cite: `Bowman.Angeli.Potts.ea.2015`.
Chúng tôi tải xuống và lưu trữ tập dữ liệu SNLI đã trích xuất trong đường dẫn `../ data / snli_1.0`.


```{.python .input  n=28}
import collections
from d2l import mxnet as d2l
from mxnet import gluon, np, npx
import os
import re
import zipfile

npx.set_np()

#@save
d2l.DATA_HUB['SNLI'] = (
    'https://nlp.stanford.edu/projects/snli/snli_1.0.zip',
    '9fcde07509c7e87ec61c640c1b2753d9041758e4')

data_dir = d2l.download_extract('SNLI')
```


<!--
### Reading the Dataset
-->

### Đọc tập dữ liệu


<!--
The original SNLI dataset contains much richer information than what we really need in our experiments.
Thus, we define a function `read_snli` to only extract part of the dataset, then return lists of premises, hypotheses, and their labels.
-->

Tập dữ liệu SNLI gốc chứa nhiều thông tin hơn những gì chúng tôi thực sự cần trong các thí nghiệm của mình.
Do đó, chúng tôi định nghĩa một hàm `read_snli` để trích xuất một phần của tập dữ liệu, sau đó trả về danh sách các tiên đề, giả thuyết và nhãn của chúng.


```{.python .input  n=66}
#@save
def read_snli(data_dir, is_train):
    """Read the SNLI dataset into premises, hypotheses, and labels."""
    def extract_text(s):
        # Remove information that will not be used by us
        s = re.sub('\\(', '', s) 
        s = re.sub('\\)', '', s)
        # Substitute two or more consecutive whitespace with space
        s = re.sub('\\s{2,}', ' ', s)
        return s.strip()
    label_set = {'entailment': 0, 'contradiction': 1, 'neutral': 2}
    file_name = os.path.join(data_dir, 'snli_1.0_train.txt'
                             if is_train else 'snli_1.0_test.txt')
    with open(file_name, 'r') as f:
        rows = [row.split('\t') for row in f.readlines()[1:]]
    premises = [extract_text(row[1]) for row in rows if row[0] in label_set]
    hypotheses = [extract_text(row[2]) for row in rows if row[0] in label_set]
    labels = [label_set[row[0]] for row in rows if row[0] in label_set]
    return premises, hypotheses, labels
```


<!--
Now let us print the first $3$ pairs of premise and hypothesis, 
as well as their labels ("0", "1", and "2" correspond to "entailment", "contradiction", and "neutral", respectively ).
-->

Bây giờ chúng ta hãy in cặp tiền đề và giả thuyết $3$ đầu tiên, cũng như nhãn của chúng ("0", "1" và "2" tương ứng với "kéo theo", "đối lập" và "trung tính").


```{.python .input  n=70}
train_data = read_snli(data_dir, is_train=True)
for x0, x1, y in zip(train_data[0][:3], train_data[1][:3], train_data[2][:3]):
    print('premise:', x0)
    print('hypothesis:', x1)
    print('label:', y)
```


<!--
The training set has about $550,000$ pairs, and the testing set has about $10,000$ pairs.
The following shows that the three labels "entailment", "contradiction", and "neutral" are balanced in 
both the training set and the testing set.
-->

Tập huấn luyện có khoảng $550,000$ cặp và tập kiểm tra có khoảng $10,000$ cặp.
Kết quả sau cho thấy ba nhãn "kéo theo", "đối lập" và "trung tính" được cân bằng trong
cả tập huấn luyện và tập kiểm tra.


```{.python .input}
test_data = read_snli(data_dir, is_train=False)
for data in [train_data, test_data]:
    print([[row for row in data[2]].count(i) for i in range(3)])
```


<!--
### Defining a Class for Loading the Dataset
-->

### Định nghĩa một lớp để tải tập dữ liệu


<!--
Below we define a class for loading the SNLI dataset by inheriting from the `Dataset` class in Gluon.
The argument `num_steps` in the class constructor specifies the length of a text sequence so that each minibatch of sequences will have the same shape. 
In other words, tokens after the first `num_steps` ones in longer sequence are trimmed, 
while special tokens “&lt;pad&gt;” will be appended to shorter sequences until their length becomes `num_steps`.
By implementing the `__getitem__` function, we can arbitrarily access the premise, hypothesis, and label with the index `idx`.
-->

Sau đây đây chúng ta định nghĩa một lớp để tải tập dữ liệu SNLI bằng cách kế thừa từ lớp `Dataset` trong Gluon.
Đối số `num_steps` trong hàm tạo của lớp lớp chỉ định độ dài của chuỗi văn bản để mỗi mini-batch của các chuỗi sẽ có cùng kích thước.
Nói cách khác, các mã thông báo sau `num_steps` đầu tiên trong chuỗi dài hơn sẽ bị cắt bỏ,
trong khi các mã thông báo đặc biệt “&lt;pad&gt;” sẽ được thêm vào các chuỗi ngắn hơn cho đến khi độ dài của chúng trở thành `num_steps`.
Bằng cách triển khai hàm `__getitem__`, chúng ta có thể tùy ý truy cập tiên đề, giả thuyết và nhãn với chỉ mục` idx`.



```{.python .input  n=115}
#@save
class SNLIDataset(gluon.data.Dataset):
    """A customized dataset to load the SNLI dataset."""
    def __init__(self, dataset, num_steps, vocab=None):
        self.num_steps = num_steps
        all_premise_tokens = d2l.tokenize(dataset[0])
        all_hypothesis_tokens = d2l.tokenize(dataset[1])
        if vocab is None:
            self.vocab = d2l.Vocab(all_premise_tokens + all_hypothesis_tokens,
                                   min_freq=5, reserved_tokens=['<pad>'])
        else:
            self.vocab = vocab
        self.premises = self._pad(all_premise_tokens)
        self.hypotheses = self._pad(all_hypothesis_tokens)
        self.labels = np.array(dataset[2])
        print('read ' + str(len(self.premises)) + ' examples')

    def _pad(self, lines):
        return np.array([d2l.truncate_pad(
            self.vocab[line], self.num_steps, self.vocab['<pad>'])
                         for line in lines])

    def __getitem__(self, idx):
        return (self.premises[idx], self.hypotheses[idx]), self.labels[idx]

    def __len__(self):
        return len(self.premises)
```

<!-- ===================== Kết thúc dịch Phần 2 ===================== -->

<!-- ===================== Bắt đầu dịch Phần 3 ===================== -->

<!--
### Putting All Things Together
-->

### Gộp tất cả lại với nhau


<!--
Now we can invoke the `read_snli` function and the `SNLIDataset` class to download the SNLI dataset and 
return `DataLoader` instances for both training and testing sets, together with the vocabulary of the training set.
It is noteworthy that we must use the vocabulary constructed from the training set as that of the testing set. 
As a result, any new token from the testing set will be unknown to the model trained on the training set.
-->

Bây giờ chúng ta có thể gọi hàm `read_snli` và lớp `SNLIDataset` để tải xuống tập dữ liệu SNLI và
trả về các thể hiện `DataLoader` cho cả tập huấn luyện và kiểm tra, cùng với từ vựng của tập huấn luyện.
Chú ý là chúng ta phải sử dụng từ vựng được xây dựng từ tập huấn luyện giống như từ vựng của tập kiểm tra.
Do đó bất kỳ mã mới nào từ bộ thử nghiệm sẽ không được mô hình được huấn luyện trên tập huấn luyện biết đến.


```{.python .input  n=114}
#@save
def load_data_snli(batch_size, num_steps=50):
    """Download the SNLI dataset and return data iterators and vocabulary."""
    num_workers = d2l.get_dataloader_workers()
    data_dir = d2l.download_extract('SNLI')
    train_data = read_snli(data_dir, True)
    test_data = read_snli(data_dir, False)
    train_set = SNLIDataset(train_data, num_steps)
    test_set = SNLIDataset(test_data, num_steps, train_set.vocab)
    train_iter = gluon.data.DataLoader(train_set, batch_size, shuffle=True,
                                       num_workers=num_workers)
    test_iter = gluon.data.DataLoader(test_set, batch_size, shuffle=False,
                                      num_workers=num_workers)
    return train_iter, test_iter, train_set.vocab
```


<!--
Here we set the batch size to $128$ and sequence length to $50$,
and invoke the `load_data_snli` function to get the data iterators and vocabulary.
Then we print the vocabulary size.
-->

Ở đây ta đặt kích thước batch là $128$ và độ dài chuỗi là $50$,
và gọi hàm `load_data_snli` để lấy các trình lặp dữ liệu và từ vựng.
Sau đó in kích thước từ vựng.


```{.python .input  n=111}
train_iter, test_iter, vocab = load_data_snli(128, 50)
len(vocab)
```


<!--
Now we print the shape of the first minibatch.
Contrary to sentiment analysis,
we have $2$ inputs `X[0]` and `X[1]` representing pairs of premises and hypotheses.
-->

Bây giờ chúng ta in kích thước của mini-batch đầu tiên. Ngược lại với phân tích sắc thái, ở đây chúng ta có $2$ đầu vào `X [0]` và `X [1]` đại diện cho các cặp tiên đề và giả thuyết.


```{.python .input  n=113}
for X, Y in train_iter:
    print(X[0].shape)
    print(X[1].shape)
    print(Y.shape)
    break
```

## Tóm tắt

<!--
* Natural language inference studies whether a hypothesis can be inferred from a premise, where both are a text sequence.
* In natural language inference, relationships between premises and hypotheses include entailment, contradiction, and neutral.
* Stanford Natural Language Inference (SNLI) Corpus is a popular benchmark dataset of natural language inference.
-->

* Suy luận ngôn ngữ tự nhiên nghiên cứu liệu một giả thuyết có thể được suy ra từ một tiên đề, trong đó cả hai đều là một chuỗi văn bản.
* Trong suy luận ngôn ngữ tự nhiên, mối quan hệ giữa các tiền đề và giả thuyết bao gồm sự kéo theo, đối lập và trung tính.
* Corpus suy diễn ngôn ngữ tự nhiên Stanford (SNLI) là một bộ dữ liệu benchmark phổ biến của suy luận ngôn ngữ tự nhiên.


## Bài tập

<!--
1. Machine translation has long been evaluated based on superficial $n$-gram matching between an output translation and a ground-truth translation.
Can you design a measure for evaluating machine translation results by using natural language inference?
2. How can we change hyperparameters to reduce the vocabulary size? 
-->

1. Dịch máy từ lâu đã được đánh giá dựa trên sự đối sánh bề ngoài $n$-gram giữa bản dịch đầu ra và bản dịch thực.
Bạn có thể thiết kế một độ đo để đánh giá kết quả dịch máy bằng cách sử dụng suy luận ngôn ngữ tự nhiên không?
2. Làm thế nào chúng ta có thể thay đổi các siêu tham số để giảm kích thước từ vựng?

<!-- ===================== Kết thúc dịch Phần 3 ===================== -->
<!-- ========================================= REVISE - KẾT THÚC ===================================-->


## Thảo luận
* [Tiếng Anh](https://discuss.d2l.ai/t/394)
* [Tiếng Việt](https://forum.machinelearningcoban.com/c/d2l)

## Những người thực hiện
Bản dịch trong trang này được thực hiện bởi:
<!--
Tác giả của mỗi Pull Request điền tên mình và tên những người review mà bạn thấy
hữu ích vào từng phần tương ứng. Mỗi dòng một tên, bắt đầu bằng dấu `*`.
Tên đầy đủ của các reviewer có thể được tìm thấy tại https://github.com/aivivn/d2l-vn/blob/master/docs/contributors_info.md
-->

* Đoàn Võ Duy Thanh
<!-- Phần 1 -->
* Nguyễn Thái Bình

<!-- Phần 2 -->
* 

<!-- Phần 3 -->
* 
