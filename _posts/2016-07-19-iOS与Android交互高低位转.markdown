---
layout: post
title:  "iOS与Android交互高低位转"
date:   2016-07-19 05:00:01 -0701
comments: true
categories: iOS
---



在与Android交互过程中，因为Android是从低位往高位读，iOS是从高位往低位读，所以交互数据需要进行转换。

>objc code
>
>/* 
>* convert big endian to little endian in C 
>*/  
>uint16_t swap_uint16( uint16_t val );  
>int16_t swap_int16( int16_t val );  
>uint32_t swap_uint32( uint32_t val );  
>int32_t swap_int32( int32_t val );  
>int64_t swap_int64( int64_t val );  
>uint64_t swap_uint64( uint64_t val );  
>  
>  
>  
>/////////////////////////////////////////////////////////////////////////////////////////  
>//! Byte swap unsigned short  
>uint16_t swap_uint16( uint16_t val )  
>{  
>    return (val << 8) | (val >> 8 );  
>}  
>  
>//! Byte swap short  
>int16_t swap_int16( int16_t val )  
>{  
>    return (val << 8) | ((val >> 8) & 0xFF);  
>}  
>  
>//! Byte swap unsigned int  
>uint32_t swap_uint32( uint32_t val )  
>{  
>    val = ((val << 8) & 0xFF00FF00 ) | ((val >> 8) & 0xFF00FF );  
>    return (val << 16) | (val >> 16);  
>}  
>  
>//! Byte swap int  
>int32_t swap_int32( int32_t val )  
>{  
>    val = ((val << 8) & 0xFF00FF00) | ((val >> 8) & 0xFF00FF );  
>    return (val << 16) | ((val >> 16) & 0xFFFF);  
>}  
>  
>int64_t swap_int64( int64_t val )  
>{  
>    val = ((val << 8) & 0xFF00FF00FF00FF00ULL ) | ((val >> 8) & 0x00FF00FF00FF00FFULL );  
>    val = ((val << 16) & 0xFFFF0000FFFF0000ULL ) | ((val >> 16) & 0x0000FFFF0000FFFFULL );  
>    val = (val << 32) | ((val >> 32) & 0xFFFFFFFFULL);  
>    return val;  
>}  
>  
>uint64_t swap_uint64( uint64_t val )  
>{  
>    val = ((val << 8) & 0xFF00FF00FF00FF00ULL ) | ((val >> 8) & 0x00FF00FF00FF00FFULL );  
>    val = ((val << 16) & 0xFFFF0000FFFF0000ULL ) | ((val >> 16) & 0x0000FFFF0000FFFFULL );  
>    val = (val << 32) | (val >> 32);  
>    return val;  
>  
>}  
>

