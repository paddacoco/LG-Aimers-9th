# Phase 2 | Online Hackathon Modeling Pipeline

온라인 해커톤에서 사용한 접근을 공개 가능한 형태로 정리한 미니 파이프라인입니다. 원본 데이터와 대회 제출 모델은 포함하지 않으며, 시간 순서를 보존한 검증과 범주형 피처 기반 확률 예측의 핵심 흐름을 재현합니다.

## What I built

- 시즌 기준 train/validation 분할로 미래 데이터 누수를 방지하는 실험 구조
- 범주형·수치형 피처를 분리해 처리하는 CatBoost 분류 파이프라인
- 확률 예측 품질을 비교할 수 있는 multiclass log loss 및 Brier score 평가
- 실험 설정과 결과를 JSON으로 저장하는 재현성 기록

## Repository structure

```text
phase2-online/
├── src/
│   ├── features.py    # 피처 목록 검증 및 범주형 결측 처리
│   ├── evaluate.py    # 확률 예측 평가 지표
│   └── train.py       # 시즌 기반 학습·검증·결과 저장
└── requirements.txt
```

## Run

```bash
pip install -r requirements.txt

python src/train.py \
  --train data/train.csv \
  --target outcome \
  --season-col season \
  --valid-season 2024 \
  --output-dir artifacts/phase2_baseline
```

`--categorical-cols`와 `--numeric-cols`를 지정하면 데이터셋의 컬럼 구성에 맞춰 명시적으로 실험할 수 있습니다. 지정하지 않으면 학습 데이터의 타입을 기준으로 합리적인 기본값을 사용합니다.

## Portfolio note

이 코드는 대회 성적을 재현하기 위한 제출 코드가 아니라, 제가 온라인 해커톤에서 적용한 **시간 기반 검증 · 범주형 데이터 모델링 · 확률 예측 평가 · 실험 기록** 방식을 보여주기 위한 공개용 예제입니다.
