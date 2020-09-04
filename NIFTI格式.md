# NIFTI文件格式
## NIFTI-1文件格式/NIFTI-2文件格式
the Neuroimaging informatics Technology Initative(神经影像学信息技术倡议)文件格式用于替换老旧的ANALYZE7.5文件格式——缺乏有关空间方向的足够信息以至于不能清晰的解释存储的数据。

***

### 相同的格式，不同的含义
以ANALYST7.5存储的单个图像需要两个文件：标头.hdr文件和实际数据.img文件。NIFTI格式保持了类似的机构，并同时允许将.hdr和.img文件扩展为单个文件.nii。同时NIFTI文件允许压缩，例如通过gzip压缩的文件扩展名为.nii.gz(单一文件)，.hdr/.img.gz。

***

### 预定义的空间和时间维度
在NIFTI格式中，预留前三个维度定义三维空间的——x,y和z——，预留第四个维度定义时间——t。剩余的维度（从第五到第七）用于其他用途。不过，第五维度仍然可具有一些预定义的用途，例如存储特定于体素的分布参数或者保存基于矢量的数据。

***

标头（header）文件概述

为了保持于ANALYZE格式的兼容性，NIFTI标头的大小保持在348字节。有些字段（fields）被重用，有些保留但被忽略，有些则完全覆盖。下表显示了每个字段的大小和简要说明。
|类型|名称|OFFSET|SIZE|描述|
|----|----|----|----|----|
int|sizeof_hdr|0B|4B|标头的大小，必须为348(bytes)
char|data_type[10]|4B|10B|不使用，兼容ANALYZE
char|db_name[18]|14B|18B|不使用，兼容ANALYZE
int|extents|32B|4B|不使用，兼容ANALYZE
short|session_error|36B|2B|不使用，兼容ANALYZE
char|regular|38B|1B|不使用，兼容ANALYZE
char|dim_info|39B|1B|编码方向（phase，frequency，slice）