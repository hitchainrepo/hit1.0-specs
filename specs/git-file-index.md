# Git File Index Specification

## Table of contents
<!-- TOC -->
- [Git File Index Specification](#git-file-index-specification)
  * [Table of contents](#table-of-contents)
  * [Description](#description)
  * [Structure](#structure)
  * [File Path](#file-path)
<!-- /TOC -->

## Description

The Git File Index is the index (directory tree) of all the files in the repository. When any Fetch is made, the Project Information File and Git File Index files are updated and the files are retrieved via the Git File Index and downloaded from IPFS.

Sample file structure:

    QmSfKU3KUBeLBZm1rPWULVRJox7GoP8eK2A5mU8frT2LAe,f00476eb3189c7acb91fa2a739bf6519f1abbcf8,objects/pack/pack-9662c80a4be4320802d1ada0aa3e5f3575611d26.idx
    QmY5G4Vv4LEynwyL1YpsvtanetrmLBJ12Gy4BPcpBSebDe,acbaef275e46a7f14c1ef456fff2c8bbe8c84724,HEAD
    QmQh2GXnMx8h6ieRkyKFgCjWkpFTjGowF1gjkZ5QPYoB2r,f7ad0a3f2d5f2e04d18a79287f9822b7d1c45d12,FETCH_HEAD
    Qmb4nG73QuXGpNgPkmh1bBkLfVB3msqBVEtufqDhKhnxBr,cf572c8b103deab8cc762bfbd8169ab74ec5d48e,objects/hit/projectinfo
    QmTTH3JEWMZDYJj92RYmTMxm6wpTGWYWpJCAD23Xzj9EKB,2cedbd99e18f92d09bfd94d82a519abb7ee1bbae,logs/refs/heads/master
    QmPmeSV9b53tnfcBANLywWvYt3GopEkUUjWtkq7cPvJJnw,7b6d1054e2e8978af2577b4ad22c128a33897124,objects/pack/pack-03518c30afc236ce2c42a14b871f07abc70bdfbb.idx
    QmSdxgQTHc9wU5j6NXWJZZxVXsm3Cvwg5wgyV3FWSPUZaa,bfc998139eea703a6ab18f65145943d800447d03,index
    QmS7XKTCWwxGe72C6Qzc1EKZyDdwATVphSc5YEZAhZV3xu,fce222cb34c18aa5e143449f8d2b58d031394398,objects/d3/9905bda05392a4858f2abc233189a22deaf8ce
    QmZoxxEkFRtha5VuuNue51g7dRG9zqXrpUNXAB2g6eXXBY,50a94f6d8030d2aa6a13b772ba89fe9203c6320e,objects/pack/pack-9662c80a4be4320802d1ada0aa3e5f3575611d26.pack
    QmehrCRe4AvryqEN3NZ5RPjjanc2tkkqgZVFu2wrTAW1KS,e2ab7fbf9d3f8569bbc9fe26517f24c57fab136f,refs/heads/master
    QmWGTsEY1jbjEHTWPyBYmTPwLoZfpNmWd9CMpGPY85q47Q,2cedbd99e18f92d09bfd94d82a519abb7ee1bbae,logs/HEAD
    QmWiyteMUV39vqpcNZDH1yodbX1CM2v2YTb1L67W7NEqv9,fd5d60b7ed072c7c9d89af9b5560dc78d0f17937,objects/pack/pack-03518c30afc236ce2c42a14b871f07abc70bdfbb.pack
    QmfYvBwEGxbgYh88cqcF1T6uY7HmYw5gitX5nv9trqJ6dC,1f5f081f6efec9f21de2b80a97ce22a9f6d9a355,config
    QmbyprgEirRZVHdECg9KpJBrB622d89S7NkivoVKKGmVhd,43266ad4e93a161b8f8189223b404ae60aff9acf,objects/14/ce66a4160d4d16e20e25d15a7f9f1fcdf197e9
    QmdYjiTrNQsa77kwhRSqRRbgU8XYo8qFvCEyRuNEPRa9Pd,f9e20a6a7d2df566609bbb2cfb5d3537f8e72180,logs/refs/remotes/origin/master
    QmcKqiY7uisVrwzZnBbLVNJ95hYy5tUGSi9H5zUGKT5dn1,f01a6ebf73401c1d5a0045b893315d5cfb537f4f,refs/remotes/origin/master
    QmNrXX5fK9pYRQ5MutcTu1QGxANbAuz6NachH55zY7GdXn,,objects/hit/gitfile.idx
    QmUnPEp3C6Wgf4PuCg6Yonojg1Jq68rZS8euHoHbd973mf,c0dfedcded2cb49bea9b7336f5492f9c3fe7fe09,objects/7e/9942abdd882c79de152be0dd15180420fa970f
    QmXotQkr6a344UW3F2kfgaTWoNZgwgZDeVvieHqVv7hSRE,f763a203393b59b0a3c61a3868fcc5fd0b795d28,info/refs
    QmWUBjGP9DJp1evT8ZWng3HTfAsEM2eMwSHy3kVcgsnkej,0e83da063db8f00fe869ba203284f6c3c0001271,objects/pack/pack-2e4388264628685633de0ac8de25612fc932a475.pack
    QmWgmU4GJtFWhvR7sagUXW6KmcLdUkjTT4Nz9wgFyKfGvc,ec674d33d17800e8cb7c5e2c7024714e2f3c7da1,objects/pack/pack-2e4388264628685633de0ac8de25612fc932a475.idx
    QmQwZy3CWdRP8RJEkdjNm6g45PUMFrs8dUB262ZPr9HZH6,d25a193b95787c176a8617eea3527aa8a0b7d89e,objects/7d/1d28f9d49f29187d24b00c7e1b3065e670f6a5
    QmQ6fGD6vLdwRECec3SEfUCHHV1q9KSgNuZ258GaNY5w6e,d426cadc796058fadca1dc47083392e2464a923b,objects/38/565077aebb0f1ae540ae9cda521efe047f127b
    QmY71uLZRhmayvdyrpagZZw5KRPh4TcnwifY2VZ8gbkBV7,094c43738b2b4a122028a7dc3acfd98b758e372a,objects/info/packs

## Structure
The structure of the file is one line for each file, each line is divided into three parts, separated by commas:
* The first part: IPFS HASH, the IPFS HASH of the file, the presence of the HASH indicates that the file has been uploaded to the IPFS server;
* Part II: HASH of Git files;
* Part III: File name, located in the .git directory;

All file contents are grouped into a file index (directory tree) and then compressed with GZIP.

## File Path
File storage location: .git/objects/hit/gitfile.idx