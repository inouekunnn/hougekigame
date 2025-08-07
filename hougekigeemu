#include <iostream>
#include <vector>
#include <string>
#include <memory>
#include <algorithm>
#include <limits>
#include <cmath>

// 的クラス（振る舞いをカプセル化）
class Target {
    int position;
    int size;
public:
    Target(int pos, int sz) : position(pos), size(sz) {}
    int getPosition() const { return position; }
    int getSize() const { return size; }
    // 砲弾が命中したか判定
    bool isHitBy(int shotPosition) const {
        return std::abs(position - shotPosition) <= size;
    }
};

// ゲーム盤を描画する関数
void drawGameBoard(int width, const std::vector<std::unique_ptr<Target>>& targets) {
    std::string board(width, '-');
    for (const auto& target : targets) {
        for (int i = -target->getSize(); i <= target->getSize(); ++i) {
            int pos = target->getPosition() + i;
            if (pos >= 0 && pos < width) board[pos] = 'T';
        }
    }
    board[0] = 'A';
    std::cout << "  ";
    for(int i = 0; i < width; ++i) std::cout << i % 10;
    std::cout << "\n A" << board.substr(1) << std::endl;
}

int main() {
    const int BOARD_WIDTH = 50;
    int score = 0;
    int shots = 10;

    // 的を準備
    std::vector<std::unique_ptr<Target>> targets;
    targets.push_back(std::make_unique<Target>(15, 1));
    targets.push_back(std::make_unique<Target>(30, 2));
    targets.push_back(std::make_unique<Target>(45, 0));

    std::cout << "=== 砲撃ゲーム開始！ ===" << std::endl;

    // ゲームループ
    while (!targets.empty() && shots > 0) {
        std::cout << "\n--------------------------------" << std::endl;
        std::cout << "スコア: " << score << " | 残弾: " << shots-- << " | 残的: " << targets.size() << std::endl;
        
        drawGameBoard(BOARD_WIDTH, targets);

        int shotPosition;
        std::cout << "砲撃座標を入力: ";
        std::cin >> shotPosition;

        bool hit = false;
        // イテレータを使って命中判定と削除を同時に行う
        for (auto it = targets.begin(); it != targets.end(); ) {
            if ((*it)->isHitBy(shotPosition)) {
                std::cout << "\n*** 命中！ ***" << std::endl;
                score += 100;
                hit = true;
                it = targets.erase(it); // 的を削除し、イテレータを次の要素に進める
            } else {
                ++it; // 命中しなかった場合、イテレータを単に進める
            }
        }
        if (!hit) std::cout << "\n--- はずれ ---" << std::endl;
    }

    // ゲーム終了
    std::cout << "\n======== ゲーム終了 ========" << std::endl;
    if (targets.empty()) std::cout << "おめでとう！全ターゲットを破壊！" << std::endl;
    else std::cout << "残念！弾切れです..." << std::endl;
    std::cout << "最終スコア: " << score << std::endl;

    return 0;
}
