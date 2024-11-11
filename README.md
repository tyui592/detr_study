# DETR Study

* End-to-End Object Detection with Transformers | DETR (2020, ECCV)
    * 트랜스포머를 검출기 문제에 활용함.
    * 데이터셋에 있는 물체 개수보다 더 많은 쿼리를 두고, 검출 결과와 GT의 매칭을 통해 학습함.
        * Cost가 최소가 되도록 매칭함, 매칭되지 않은 검출 결과는 `no_object` label로 할당함.
* Deformable DETR Deformable Transformers for End-to-End Object Detection | Deformable DETR (2021, ICLR Oral)
    * Deformable Conv을 transformer attention에 적용.
    * Query 당 key를 4개 (x scale 4개) 보기 때문에 연산량이 매우 줄어듬.
* Efficient DETR
* Rethinking Transformer-based Set Prediction for Object Detection | TSP (2021, ICCV)
    * encoder only detr
* Fast Convergence of DETR with Spatially Modulated Co-Attention | SMCA (2021, ICCV)
    * Query에서 object의 center(x,y)와 scale (w,h) estimation해서 활용.
    * x,y,w,h로 가우시안 커널 G 만들어서 attention weight를 조절함
        * 더해서 조절한다: softmax(K^T Q + logG)
    * multi-head를 위해서 head마다 x,y offset을 위한 레이어 추가해서 G_i 생성
    * multi-scale
        * 연산량으로 인해, feature들은 intra-scale로 encoder에 통과시킨다.
        * Query로 스케일 weight를 estimation해서 weighted sum한다.
* Conditional DETR for Fast Training Convergence | Conditional DETR (2021, ICCV)
    * Attention 계산시 Content embedding과 position embedding으로 나누어서 생각.
    * 그 중 position과 연관된 conditional spatial query 제안.
        * obj query로부터 x,y coord 계산하고, 이로 sinusoidal encoding을 계산하여 활용
        * content 정보도 활용하기 위해 decoder embedding으로부터 vector 계산하여 element-wise multiplication 함.
* Dab-detr Dynamic anchor boxes are better queries for detr | DAB DETR (2022, ICLR)
    * Conditional detr은 x,y coordinate만 고려하는데, size(w,h) 정보도 고려하자.
    * anchor (box, coordinates, xywh) 자체를 query로 정의.
        * 이를 통해, positional attention 계산할때 크기를 고려할 수 있고
        * anchor를 layer wise로 update할 수 있음.
* Anchor detr Query design for transformer-based detector | Anchor DETR (2022, AAAI)
    * #todo sinusodial encoding 어떻게 정의했는지 조사하기.
    * self-attention의 complexity를 개선한 방법들: (Ma et al. 2021; Shen et al. 2021)
    * Positional Query를 center position (x,y)으로 정의하고 MLP 통과시켜서 embedding을 얻음.
    * One position에서 multiple prediction을 위해, pattern embedding을 학습함.
        * position embedding에 pattern embedding을 더해서 N_q x N_p 개를 입력함
    * Row Column Decoupled Attention을 제안, global avg pool으로 row, col으로 각각 줄여서 attn. 계산. 성능 유지하며 연산량 줄임.
* Dino Detr with improved denoising anchor boxes for end-to-end object detection | DINO (2023, ICLR)
    * htc++
    * Object365 dataset: 
* H-DETR (2023, CVPR)
* Group DETR Fast DETR Training with Group-Wise One-to-Many Assignment | Group DETR (2023, ICCV)
* DETRs with Collaborative Hybrid Assignments Training | Co-DETR (2023, ICCV)
* DETRs Beat YOLOs on Real-time Object Detection | RT-DETR (2024, CVPR)
