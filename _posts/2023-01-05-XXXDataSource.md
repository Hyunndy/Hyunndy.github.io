---
title: "[iOS] XXXDataSource들 정리"
excerpt: "iOS에 등장하는 여러 DataSource를 정리"

categories:
  - iOS
tags:
  - [iOS, DataSource]

permalink: /categories1/post-name-here/iOSDataSource

toc: true
toc_sticky: true

date: 2023-01-05
last_modified_at: 2021-10-09
---

## 🦥 본문

# iOS의 XXXDataSource 정리

TableView, CollectionView를 구성할 때 기본 DataSource 프로토콜을 채택해서 사용하면 지겨운 보일러 플레이트 코드를 만나게된다.

새로운거 없을까(나온지 오래된 기술이지만) 하다가 보니...
애플, Rx에서 DataSource를 새롭게 사용할 수 있는 개념을 만들었다고한다.
그래서 각자 스터디하고 깔짝깔짝 프로젝트에 적용해보니, 기본 개념이 비슷하고 쓰는 용어가 비슷해 나도모르게 개념이 섞이는 느낌이 들었다.

이 포스팅에서는 2개를 간단명료하게 한 페이지에 정리해놓음으로써 섞여있는 개념을 명확하게 정리하고자 한다.

## DiffableDataSource

WWDC19에서 발표한 Apple의 DataSource
변경된 부분만 새로 다시 그린다.
기존과 다르게 protocol이 아닌 Generic Class.

###필요한 개념
* (GenericType) SectionIdentifierType: Hashable
* (GenericType) ItemIdentidifierType: Hashable
* SnapShot

###예시
    class UITableViewDiffableDataSource<SectionIdentifierType, ItemIdentifierType> : NSObject where SectionIdentifierType : Hashable, ItemIdentifierType : Hashable

    struct NSDiffableDataSourceSnapshot<SectionIdentifierType, ItemIdentifierType> where SectionIdentifierType : Hashable, ItemIdentifierType : Hashable

     var dataSource: UICollectionViewDiffableDataSource<Int, String>!

## RxDataSource

RxSwift커뮤니티에서 만든 DataSource
바인딩할 데이터를 Observable 형태로 만들고, DataSource에 bind(tableview.rx.items(dataSource: dataSource)) 해준다.

### 종류
* RxTableViewSectionedReloadDataSource
* RxTableViewSectionedAnimatedDataSource (애니메이션이 필요할 때)

### 필요한 개념
* (프로토콜) SectionModelType
* (typealias) Item

* (프로토콜) AnimatableSectionModelType
* (프로토콜) IdentifiableType
