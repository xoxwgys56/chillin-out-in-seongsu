# ImageNet Classification with Deep Neural Networks(: AlexNet)

2021-06-10, [kkimlim2](https://github.com/kkimlim2)

> copied from https://hyelimkungkung.tistory.com/22

## Header

 알렉스 넷은 ImageNet LSVRC-2010이라는 이미지 분류 대회에서 획기적으로 오류율을 낮춰 모두의 주목을 받았던 모델이다. 딥러닝을 성공적으로 활용했다고 평가받는 알렉스 넷에 대해서 며칠동안... 계속 봐서 쭈글쭈글 해진 공부한 내용을 포스팅 하도록 하겠다..

 논문 제목을 검색하면 바로 볼 수 있다.

 본 논문이 나온 시점은 바야흐로 2012년.. 초5 무렵이다


## Introduction

(논문 전체의 요약을 담고 있다 보통 서론은 그렇게 안 쓰지 않나?)

 많은 고해상도 이미지를 분류하기 위해서는 그만큼 큰 학습을 수용할 수 있는 모델이 필요함= > 그래서 CNN 활용함

(∵ 앞 포스팅에서도 말했듯이, CNN에서는 이미지의 공간적 정보를 학습하기 위해서 kernel을 이용함 그렇기 때문에 합성곱 층에서 사용하는 가중치의 갯수는 커널의 크기로 고정되어 있고, 그 크기는 사용자가 설정할 수 있음. 만약 그렇지 않고 그냥 다층 퍼셉트론을 사용한다면 input size * hidden layer 의 계산결과 만큼 가중치가 필요함) 

 ![note](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FoSSwP%2Fbtq4c2ngIG3%2FxKLeHwfZEcXRCDxISji010%2Fimg.png)

거기에 더불어서, 몇가지 알렉스 넷에서는 성능을 높이고 학습 시간을 줄이기 위해서 '새롭고 특이한 기법 new and unusual features)' 과 과적합 방지를 위해서 '효과적인 기법effective techniques'을 사용했다. 자세한 건 section 3와 4에서 다룬다. 

 또, 현재 사용하고 있는 GPU는 GTX 580 3GV GPUs 라고 한다. 현재는 이것보다 더 발달된 GPU가 많아서, 실제로 이 알렉스넷에 사용됐던 몇 기법들은 안 쓴다고 한다.. 

 GPU, CPU 의 차이로는 GPU는 단순 계산에 적합하다고만 알면 될 것 같다. CPU는 보다 복잡한 계산에.

 구조를 미리 알면 나중에 볼 때 유용할 것 같아서 나중에 나오는 figure지만 미리 올린다. 

![note](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FmirJt%2Fbtq4cGY4BO5%2FG6qYaA8lGzYsv3FJ3GwyEk%2Fimg.png)

> 자세한 내용은 블로그 참고

---

## References

0. 무엇보다도 핵심인 원문 : papers.nips.cc/paper/2012/file/c399862d3b9d6b76c8436e924a68c45b-Paper.pdf

1. 원문도 그대로 실어서 해석에도 도움이 되고 기타 부가 설명도 많아서 좋은 포스팅!! : 89douner.tistory.com/60

2. data augmentation 에 대해서 도움이 된 글: blog.naver.com/PostView.nhn?blogId=intelliz&logNo=221743351934

3. 이미지에 대한 이해(픽셀에 관해서 알고 싶다면): twlab.tistory.com/23

4. section 5와 관련해서 보기 좋은 포스팅: hiddenbeginner.github.io/deeplearning/paperreview/2019/12/29/paper_review_AdamW.html

5. 이미지 부자: learnopencv.com/understanding-alexnet/

6.  (구현) nn.Dropout(inplace=True)에 대해서 헤매게 한 deep-learning-study.tistory.com/376

7.  (구현) wolfy.tistory.com/241