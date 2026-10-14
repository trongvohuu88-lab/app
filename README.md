import { useState } from 'react';
import {
    View,
    Text,
    Image,
    FlatList,
    ScrollView,
    TouchableOpacity,
} from 'react-native';
import { SafeAreaView } from 'react-native-safe-area-context';
import { LinearGradient } from 'expo-linear-gradient';
import { Ionicons } from '@expo/vector-icons';

import products from '../../data/products.json';

const categories = ['Áo thun', 'Quần Jean', 'Sơ mi', 'Quần tây', 'Giày lười'];
const formatVND = (n) => `${n.toLocaleString('vi-VN')} đ`;

// Thêm 1 phần tử rỗng nếu số sản phẩm lẻ, để item cuối không bị giãn full hàng
const listData =
    products.length % 2 === 0
        ? products
        : [...products, { id: '__empty__', empty: true }];

function ProductItem({ item }) {
    if (item.empty) return <View className="flex-1" />;

    return (
        <View className="flex-1 bg-white rounded-2xl overflow-hidden shadow-md">
            <Image source={{ uri: item.image }} className="w-full h-36 bg-gray-200" />
            <View className="p-3">
                <Text className="text-base mb-1.5" numberOfLines={1}>
                    {item.name}
                </Text>
                <Text className="text-[#0a8a1f] font-bold text-[15px]">
                    {formatVND(item.price)}
                </Text>
                {item.oldPrice > item.price && (
                    <Text className="text-gray-400 text-[13px] line-through">
                        {formatVND(item.oldPrice)}
                    </Text>
                )}
            </View>
        </View>
    );
}

function Header({ selected, onSelect }) {
    return (
        <View>
            <View className="flex-row justify-between items-center pt-2.5 pb-5">
                <TouchableOpacity>
                    <Ionicons name="menu-outline" size={30} color="#000" />
                </TouchableOpacity>
                <View className="flex-row items-center gap-1.5">
                    <Ionicons name="search-outline" size={24} color="#000" />
                    <Text className="text-base">Võ Hữu Trọng</Text>
                </View>
            </View>

            <Text className="text-[#0a8a1f] text-[22px] font-extrabold mt-2.5 mb-3">
                Danh mục sản phẩm
            </Text>

            <ScrollView
                horizontal
                showsHorizontalScrollIndicator={false}
                className="mb-5"
                contentContainerClassName="gap-2.5"
            >
                {categories.map((category) => {
                    const active = selected === category;
                    return (
                        <TouchableOpacity
                            key={category}
                            onPress={() => onSelect(category)}
                            className={`bg-white rounded-2xl py-2.5 px-5 border-2 shadow-sm ${
                                active ? 'border-[#0a8a1f]' : 'border-transparent'
                            }`}
                        >
                            <Text
                                className={`text-base ${
                                    active ? 'text-[#0a8a1f] font-semibold' : 'text-black'
                                }`}
                            >
                                {category}
                            </Text>
                        </TouchableOpacity>
                    );
                })}
            </ScrollView>
        </View>
    );
}

export default function Bai1() {
    const [selected, setSelected] = useState(categories[0]);

    return (
        <LinearGradient
            colors={['#f8c6dc', '#f4bfd8', '#c9b6e0', '#7fd3f0']}
            locations={[0, 0.35, 0.7, 1]}
            style={{ flex: 1 }}
        >
            <SafeAreaView className="flex-1">
                <FlatList
                    data={listData}
                    keyExtractor={(item) => String(item.id)}
                    numColumns={2}
                    renderItem={({ item }) => <ProductItem item={item} />}
                    ListHeaderComponent={<Header selected={selected} onSelect={setSelected} />}
                    columnWrapperClassName="gap-3 mb-3"
                    contentContainerClassName="px-3.5 pb-8"
                    showsVerticalScrollIndicator={false}
                />
            </SafeAreaView>
        </LinearGradient>
    );
}
[
  {
    "id": 1,
    "name": "Bình giữ nhiệt inox",
    "price": 250000,
    "image": "https://images.unsplash.com/photo-1602143407151-7111542de6e8?w=500"
  },
  {
    "id": 2,
    "name": "Đèn bàn LED",
    "price": 320000,
    "image": "https://images.unsplash.com/photo-1507473885765-e6ed057f782c?w=500"
  },
  {
    "id": 3,
    "name": "Loa Bluetooth mini",
    "price": 590000,
    "image": "https://images.unsplash.com/photo-1608043152269-423dbba4e7e1?w=500"
  },
  {
    "id": 4,
    "name": "Bàn phím không dây",
    "price": 650000,
    "image": "https://images.unsplash.com/photo-1587829741301-dc798b83add3?w=500"
  },
  {
    "id": 5,
    "name": "Chuột không dây",
    "price": 350000,
    "image": "https://images.unsplash.com/photo-1527814050087-3793815479db?w=500"
  },
  {
    "id": 6,
    "name": "Tai nghe chụp tai",
    "price": 850000,
    "image": "https://images.unsplash.com/photo-1505740420928-5e560c06d30e?w=500"
  },
  {
    "id": 7,
    "name": "Sạc dự phòng 10000mAh",
    "price": 450000,
    "image": "https://images.unsplash.com/photo-1609592424714-ea1c7f9e6a0a?w=500"
  },
  {
    "id": 8,
    "name": "Giá đỡ điện thoại",
    "price": 150000,
    "image": "https://images.unsplash.com/photo-1601784551446-20c9e07cdbdb?w=500"
  },
  {
    "id": 9,
    "name": "Balo laptop",
    "price": 550000,
    "image": "https://images.unsplash.com/photo-1553062407-98eeb64c6a62?w=500"
  },
  {
    "id": 10,
    "name": "Túi tote canvas",
    "price": 180000,
    "image": "https://images.unsplash.com/photo-1590874103328-eac38a683ce7?w=500"
  },
  {
    "id": 11,
    "name": "Ví da nhỏ",
    "price": 280000,
    "image": "https://images.unsplash.com/photo-1627123424574-724758594e93?w=500"
  },
  {
    "id": 12,
    "name": "Đồng hồ điện tử",
    "price": 750000,
    "image": "https://images.unsplash.com/photo-1523275335684-37898b6baf30?w=500"
  },
  {
    "id": 13,
    "name": "Kính mát",
    "price": 300000,
    "image": "https://images.unsplash.com/photo-1511499767150-a48a237f0083?w=500"
  },
  {
    "id": 14,
    "name": "Ô dù gấp gọn",
    "price": 220000,
    "image": "https://images.unsplash.com/photo-1515694346937-94d85e41e6f0?w=500"
  },
  {
    "id": 15,
    "name": "Nến thơm",
    "price": 190000,
    "image": "https://images.unsplash.com/photo-1603006905003-be475563bc59?w=500"
  },
  {
    "id": 16,
    "name": "Máy khuếch tán tinh dầu",
    "price": 420000,
    "image": "https://images.unsplash.com/photo-1608571423902-eed4a5ad8108?w=500"
  },
  {
    "id": 17,
    "name": "Cây cảnh để bàn",
    "price": 160000,
    "image": "https://images.unsplash.com/photo-1485955900006-10f4d324d411?w=500"
  },
  {
    "id": 18,
    "name": "Chậu cây ceramic",
    "price": 230000,
    "image": "https://images.unsplash.com/photo-1485955900006-10f4d324d411?w=500"
  },
  {
    "id": 19,
    "name": "Bộ ly thủy tinh",
    "price": 280000,
    "image": "https://images.unsplash.com/photo-1581781870027-04212e231e96?w=500"
  },
  {
    "id": 20,
    "name": "Bình hoa ceramic",
    "price": 350000,
    "image": "https://images.unsplash.com/photo-1612196808214-b8e1d6145a8c?w=500"
  },
  {
    "id": 21,
    "name": "Thớt gỗ nhà bếp",
    "price": 180000,
    "image": "https://images.unsplash.com/photo-1556911220-bff31c812dba?w=500"
  },
  {
    "id": 22,
    "name": "Bộ dao nhà bếp",
    "price": 480000,
    "image": "https://images.unsplash.com/photo-1593618998160-e34014e67546?w=500"
  },
  {
    "id": 23,
    "name": "Nồi chiên không dầu",
    "price": 1850000,
    "image": "https://images.unsplash.com/photo-1585515320310-259814833e62?w=500"
  },
  {
    "id": 24,
    "name": "Máy xay sinh tố",
    "price": 720000,
    "image": "https://images.unsplash.com/photo-1570222094114-d054a817e56b?w=500"
  },
  {
    "id": 25,
    "name": "Bình cà phê French Press",
    "price": 390000,
    "image": "https://images.unsplash.com/photo-1495474472287-4d71bcdd2085?w=500"
  },
  {
    "id": 26,
    "name": "Sổ tay bìa da",
    "price": 170000,
    "image": "https://images.unsplash.com/photo-1517842645767-c639042777db?w=500"
  },
  {
    "id": 27,
    "name": "Bút máy cao cấp",
    "price": 260000,
    "image": "https://images.unsplash.com/photo-1585336261022-680e295ce3fe?w=500"
  },
  {
    "id": 28,
    "name": "Đèn ngủ cảm ứng",
    "price": 380000,
    "image": "https://images.unsplash.com/photo-1513506003901-1e6a229e2d15?w=500"
  },
  {
    "id": 29,
    "name": "Gối tựa lưng",
    "price": 240000,
    "image": "https://images.unsplash.com/photo-1584100936595-c0654b55a2e2?w=500"
  },
  {
    "id": 30,
    "name": "Chăn sofa mềm",
    "price": 450000,
    "image": "https://images.unsplash.com/photo-1580301762395-21ce6a2d6f5f?w=500"
  }
]
